# OMEN V1 — Codebase Audit Report

**Tanggal**: 2026-09-20
**Cakupan**: Seluruh codebase `/omen` (web + contracts)
**Referensi**: `update-brief-1.md` (§01–§50, §51, §2.1–§2.8)
**Tujuan**: Identifikasi bug, pelanggaran prinsip, dan gap implementasi — **TANPA perbaikan kode**

---

## BAGIAN 1 — Logical Bugs & Potensi Error Runtime

### 🔴 CRITICAL

#### BUG-01: Smart Contract Mismatch — Dua Arsitektur Contract Berbeda Hidup Bersamaan

**File terdampak**:
- `contracts/contracts/PredictionMarket.sol` — kontrak "lama" (monolitik, `yes/no`, `bool side`)
- `contracts/src/OmenFactory.sol` + `contracts/src/OmenMarket.sol` — kontrak "baru" (factory pattern, `AGREE/DISAGREE`, `uint8 outcome`)

**Masalah**: Dua arsitektur smart contract hidup bersamaan di repository. Frontend hooks (`useAdminCreateMarket`, `useAdminResolveMarket`, `usePlaceBet`, `useClaimPayout`) menggunakan **`PREDICTION_MARKET_ABI`** (kontrak PredictionMarket.sol lama) untuk operasi via factory address, sekaligus menggunakan **`OMEN_MARKET_ABI`** untuk operasi via market address. Ini menciptakan ambiguitas kritis:

| Hooks | ABI yang Dipakai | Fungsi yang Dipanggil |
|---|---|---|
| `useAdminCreateMarket` | `PREDICTION_MARKET_ABI` | `createMarket(title, deadline)` |
| `useAdminResolveMarket` | `PREDICTION_MARKET_ABI` | `resolveMarket(marketId, bool)` / `cancelMarket(marketId)` |
| `usePlaceBet` (factory path) | `PREDICTION_MARKET_ABI` | `placeBet(marketId, side)` |
| `usePlaceBet` (market path) | `OMEN_MARKET_ABI` | `depositAgree()` / `depositDisagree()` |
| `useClaimPayout` (factory path) | `PREDICTION_MARKET_ABI` | `claim(marketId)` |
| `useClaimPayout` (market path) | `OMEN_MARKET_ABI` | `claimPayout()` |
| `useClaim` | `OMEN_MARKET_ABI` | `claimPayout()` |

**Risiko**: Jika deployed contract di testnet adalah `OmenFactory` + `OmenMarket` (arsitektur baru), semua panggilan melalui `PREDICTION_MARKET_ABI` ke factory address akan **revert** karena fungsi `placeBet(marketId, bool)`, `resolveMarket(marketId, bool)`, dll. **tidak ada** di OmenFactory.sol yang deployed. Sebaliknya, jika yang di-deploy adalah `PredictionMarket.sol`, maka panggilan via market address ke `depositAgree()`/`claimPayout()` akan gagal.

**Dampak**: Seluruh alur on-chain (create → bet → resolve → claim) bisa fail total tergantung mana yang di-deploy.

---

#### BUG-02: `resolution-engine.ts` Memanggil `resolveMarket(outcomeUint)` dengan Argumen Tunggal, Tapi `OMEN_MARKET_ABI` Menerima `uint8`

**File**: `web/lib/market/resolution-engine.ts` (line 107–114)

```typescript
const outcomeUint = outcome === "AGREE" ? 1 : outcome === "DISAGREE" ? 2 : 3;
const hash = await walletClient.writeContract({
  address: market.contract_address as Address,
  abi: OMEN_MARKET_ABI as any,
  functionName: "resolveMarket",
  args: [outcomeUint],
});
```

**Masalah**: `OmenMarket.resolveMarket` menerima `Outcome` enum sebagai `uint8` (0=UNRESOLVED, 1=AGREE, 2=DISAGREE, 3=VOID). Backend mengirim `outcomeUint` yang nilainya 1/2/3. Ini secara teori **benar** untuk OmenMarket. Namun, `useAdminResolveMarket` hook memanggil `resolveMarket(marketId, bool)` via `PREDICTION_MARKET_ABI` — signature yang **berbeda total** (2 args vs 1 arg). Kedua jalur ini saling bertentangan.

---

#### BUG-03: Race Condition pada Pool Update — Bets Bisa Double-Count

**File**: `web/app/api/bets/index/route.ts` (line 122–133) dan `web/app/api/markets/[id]/position/route.ts` (line 131–143)

**Masalah**: Dua endpoint berbeda (`/api/bets/index` dan `/api/markets/[id]/position`) sama-sama meng-update `agree_pool`/`disagree_pool` di tabel `markets`. Frontend hook `usePlaceBet` memanggil `/api/bets/index`, tapi jika ada caller lain yang menggunakan `/api/markets/[id]/position`, pool bisa di-increment dua kali. Tidak ada mekanisme locking atau transaksi atomik.

Kedua endpoint juga melakukan **read-then-write** non-atomic: baca current pool → hitung new pool → update. Jika dua request datang bersamaan, keduanya baca pool yang sama dan masing-masing menghasilkan update yang "menimpa" increment lainnya (lost update).

---

#### BUG-04: `resolveMarket` di Resolution Engine Tidak Membedakan `VOID` vs Normal Resolve di On-Chain

**File**: `web/lib/market/resolution-engine.ts` (line 107)

```typescript
const outcomeUint = outcome === "AGREE" ? 1 : outcome === "DISAGREE" ? 2 : 3;
```

Ketika outcome = `VOID`, kode mengirim `3` ke `resolveMarket(3)` di OmenMarket. Tapi kontrak OmenMarket membedakan `resolveMarket(Outcome.VOID)` yang mengubah status ke `VOID`, dari `voidMarket()` yang merupakan fungsi terpisah. `resolveMarket(3)` **seharusnya bekerja** karena kontrak mengecek `outcome == Outcome.VOID` (L127). Namun, perlu dicatat bahwa kontrak mengecek `block.timestamp < closeTime → revert MarketNotClosed()` — jadi VOID via `resolveMarket` hanya bisa dilakukan setelah deadline. Untuk emergency void sebelum deadline, harus pakai `voidMarket()`, tapi resolution engine **tidak pernah** memanggil `voidMarket()`.

---

### 🟡 WARNING

#### BUG-05: `oracle_snapshots` Query Tidak Filter `snapshot_type`

**File**: `web/lib/market/resolution-engine.ts` (line 59–63)

```typescript
const { data: startSnapshot } = await supabase
  .from("oracle_snapshots")
  .select("*")
  .eq("market_id", market.id)
  .maybeSingle();
```

**Masalah**: Mengambil snapshot tanpa filter `snapshot_type = "START"`. Jika ada beberapa snapshot (START, END, DISPLAY), `maybeSingle()` bisa gagal (throw error) karena menemukan lebih dari 1 row. Atau, yang dikembalikan bisa jadi snapshot bertipe `DISPLAY` yang bukan start price.

---

#### BUG-06: `creator_profiles` Author Matching Tidak Konsisten

**File**: `web/lib/market/resolution-engine.ts` (line 148–153) dan `web/app/api/markets/[id]/resolve/route.ts` (line 144–150)

**Masalah**: Kode mencari `creator_profiles` berdasarkan `wallet_address = belief.author.toLowerCase()`. Tapi `belief.author` sering berisi handle social media (misal `@elonmusk`), bukan wallet address. Jadi `creator_profiles.wallet_address` **tidak akan match** dengan `@elonmusk`.toLowerCase(). Profile tidak akan pernah di-update resolved/correct count, membuat reputation system tidak bekerja.

---

#### BUG-07: `isCorrect` Selalu Dihitung Sebagai `outcome === "AGREE"`

**File**: `web/lib/market/resolution-engine.ts` (line 156) dan `web/app/api/markets/[id]/resolve/route.ts` (line 153)

```typescript
const isCorrect = outcome === "AGREE";
```

**Masalah**: Ini asumsi bahwa creator selalu "benar" jika outcome = AGREE. Tapi dalam update-brief, creator hanya mengkonfirmasi bahwa belief itu miliknya — bukan bahwa hasilnya AGREE. Logika `isCorrect` seharusnya berdasarkan apakah creator berdiri di sisi yang menang, bukan secara default AGREE = correct.

---

#### BUG-08: `CHAINLINK_PRICE_FEEDS` untuk Robinhood Chain Pakai Feed Address Sepolia

**File**: `web/lib/constants.ts` (line 28–33)

```typescript
[ROBINHOOD_TESTNET_CHAIN_ID]: {
  ETH: CHAINLINK_ETH_USD_FEED,  // ← address Sepolia!
  BTC: CHAINLINK_BTC_USD_FEED,
  ...
}
```

**Masalah**: Robinhood Chain Testnet menggunakan feed address yang sama dengan Sepolia. Ini **salah** — Chainlink feed addresses berbeda per chain. Jika market di-deploy di Robinhood Chain, panggilan ke feed address Sepolia akan gagal karena contract tidak ada di Robinhood Chain.

Referensi brief §2.2: *"cek https://docs.chain.link/data-feeds untuk network Robinhood Chain — pastikan feed SOL/USD & ETH/USD ada"*. Ini belum dilakukan.

---

#### BUG-09: `robinhoodChain` Didefinisikan 4x di Tempat Berbeda

**File terdampak**:
1. `web/lib/constants.ts` (line 37) — exported sebagai `robinhoodChain`
2. `web/lib/wagmi.ts` (line 12) — didefinisikan ulang sebagai `robinhoodTestnet`
3. `web/lib/rpc-decoder.ts` (line 43) — didefinisikan ulang lokal
4. `web/scripts/sync-testnet-markets.ts` (line 30) — didefinisikan ulang lokal
5. `web/scripts/seed-testnet-activity.ts` (line 28) — didefinisikan ulang lokal

**Masalah**: Melanggar DRY. Jika RPC URL berubah, harus diubah di 4+ tempat. Sudah ada definisi kanonik di `constants.ts`, tapi file lain tidak menggunakannya.

---

#### BUG-10: `EVM_ADDRESS_REGEX` Diduplikasi di 5+ File

**File terdampak**:
- `web/app/api/wallet/connect/route.ts`
- `web/app/api/bets/route.ts`
- `web/app/api/bets/index/route.ts`
- `web/app/api/markets/[id]/position/route.ts`
- `web/app/api/markets/[id]/claim/route.ts`
- `web/app/api/beliefs/[id]/confirm/route.ts`

**Masalah**: Konstanta `const EVM_ADDRESS_REGEX = /^0x[a-fA-F0-9]{40}$/;` di-copy-paste di setiap file. Pelanggaran DRY.

---

#### BUG-11: `calculateSettlementPool` Default Fee 200 BPS (2%) — Brief Bilang Default 0

**File**: `web/lib/market/resolution-helper.ts` (line 26)

```typescript
protocolFeeBps = 200
```

**Masalah**: Update-brief §04 menyebutkan *"Protocol fee bisa diterapkan nanti; V1 sebaiknya configurable, default 0 di testnet"*. Tapi default-nya 200 BPS (2%), bukan 0. Fee ini mengurangi distributable pool dan menyimpan potongan tanpa mekanisme withdrawal — fee "menghilang" karena tidak ada treasury contract.

---

#### BUG-12: `useClaim` Hook Memanggil `claimPayout` tapi `PredictionMarket.sol` Punya Fungsi `claim`, Bukan `claimPayout`

**File**: `web/hooks/useClaim.ts` (line 39)

```typescript
functionName: "claimPayout",
```

**Masalah**: `useClaim` memanggil `claimPayout()` pada `OMEN_MARKET_ABI` — ini benar untuk `OmenMarket.sol`. Tapi `useClaimPayout` pada factory path memanggil `claim(marketId)` via `PREDICTION_MARKET_ABI` — ini benar untuk `PredictionMarket.sol`. Kembali ke BUG-01: dua jalur kontrak yang saling bertentangan.

---

#### BUG-13: `useCreatorConfirm` EIP-712 Domain Mismatch dengan Backend Verification

**File frontend**: `web/hooks/useCreatorConfirm.ts` (line 47–52)
**File backend**: `web/lib/eip712/confirmation.ts` (line 21–25)

| Property | Frontend (hook) | Backend (verifier) |
|---|---|---|
| `domain.name` | `"Omen Belief Protocol"` | `"OMEN"` |
| `domain.version` | `"1"` | `"1"` |
| `domain.verifyingContract` | `factoryAddress` | **tidak ada** |
| `types.primaryType` | `"ConfirmBelief"` | `"BeliefConfirmation"` |
| `types.fields` | `beliefId, creator, statement, timestamp` | `beliefId, statement, timestamp` |

**Dampak**: Signature yang di-sign di frontend **tidak akan pernah terverifikasi** di backend karena domain name, primary type, dan fields berbeda. Creator confirmation EIP-712 **broken**.

---

### 🟡 MINOR

#### BUG-14: `markets` POST Menyisipkan Status `"active"` (lowercase), Tapi Query Filter Menggunakan `"OPEN"` (uppercase)

**File**: `web/app/api/markets/route.ts`
- POST insert: `status: "active"` (line 240)
- GET query: `.in("status", ["OPEN", "open", "active"])` (line 29)

**Masalah**: Inkonsistensi status naming. Beberapa tempat pakai `"active"`, lain pakai `"OPEN"`. `resolution-engine.ts` hanya check `["OPEN", "active"]`, tapi seharusnya ada satu source of truth.

---

#### BUG-15: `seed.sql` Berisi Data Fake (tapi bukan production code)

**File**: `web/db/seed.sql` (27KB)

**Catatan**: File ini berisi data seed untuk development. Bukan mock di production, tapi perlu dicatat bahwa file ini besar dan mengandung data dummy yang tidak harus di-deploy ke Supabase production.

---

## BAGIAN 2 — DRY & SOLID Principles Violations

### Pelanggaran DRY

| # | Masalah | File Terdampak |
|---|---|---|
| DRY-01 | `robinhoodChain` didefinisikan 4x | `constants.ts`, `wagmi.ts`, `rpc-decoder.ts`, 2 scripts |
| DRY-02 | `EVM_ADDRESS_REGEX` di-copy-paste 6x | 6 API route files |
| DRY-03 | `isAuthorizedAdmin()` fungsi identik di-copy-paste | `markets/route.ts`, `markets/[id]/resolve/route.ts` |
| DRY-04 | `sepoliaChain` didefinisikan ulang di `rpc-decoder.ts` | `rpc-decoder.ts` (line 29) padahal sudah ada `sepolia` dari `viem/chains` |
| DRY-05 | Creator profile update logic di-copy-paste | `resolution-engine.ts` (line 147–167) dan `resolve/route.ts` (line 132–168) — kode identik |
| DRY-06 | Market settlement insert logic duplikat | `resolution-engine.ts` (line 188–198) dan `resolve/route.ts` (line 195–210) |
| DRY-07 | Resolution record insert logic duplikat | `resolution-engine.ts` (line 170–182) dan `resolve/route.ts` (line 171–188) |
| DRY-08 | `PREDICTION_MARKET_ABI` inline di `contracts.ts` (571 lines) | Padahal sudah ada `PredictionMarket.json` file |
| DRY-09 | `contracts.ts` re-export semua dari `constants.ts` | File 571-line yang mayoritas cuma re-export + inline ABI |
| DRY-10 | `evaluateOracleCondition` dan `evaluateResolution` — dua fungsi melakukan hal serupa | `resolution-helper.ts` vs `chainlink.ts` |
| DRY-11 | `getPublicClientForChain` didefinisikan di `chainlink.ts` dan `rpc-decoder.ts` | Dua file berbeda |

### Pelanggaran SOLID

| # | Prinsip | Masalah |
|---|---|---|
| SRP-01 | Single Responsibility | `contracts.ts` melanggar SRP: re-exports, ABI definition, utility functions, semua dalam satu file. |
| SRP-02 | Single Responsibility | `resolution-engine.ts` mengurus: oracle fetch, on-chain resolve, DB market update, DB belief update, DB creator profile update, DB resolution insert, DB settlement insert — semua dalam satu fungsi. |
| OCP-01 | Open/Closed | Resolution type handling (`evaluateOracleCondition`) menggunakan if-else chain. Menambah resolution type baru memerlukan modifikasi fungsi existing. |
| DIP-01 | Dependency Inversion | API routes langsung memanggil `getSupabaseAdminClient()` — tidak ada abstraction layer. Sulit di-test dan di-swap. |
| ISP-01 | Interface Segregation | `Market` type terlalu gemuk — banyak optional fields (`?`). Tidak ada type terpisah untuk create vs read vs update. |

---

## BAGIAN 3 — Verifikasi Update-Brief Per Nomor

### §01–02: Product Thesis & V1 Principle
✅ Belief market model implemented. Core loop ada: belief detection → market → AGREE/DISAGREE → pool → resolution.
⚠️ Brief menyebutkan "Jangan bangun: AMM kompleks, leverage, perp..." — V1 memang tidak memiliki ini. Sesuai.

### §03: Market Model
✅ 2 sisi (AGREE/DISAGREE) diimplementasi.

### §04: Pool Mechanism
✅ Shared pari pool model — dana masuk ke pool sesuai side.
🔴 **Payout formula benar** di smart contract (`OmenMarket.sol` line 190) tapi **protocol fee default 200 BPS** (seharusnya 0 di testnet, brief: "default 0 di testnet").

### §05: Market Odds
⚠️ **CONSENSUS (participant-based)** dan **CAPITAL distribution** terpisah — diimplementasi di `markets/route.ts` (`capitalConsensus`, `agree_participants`, `disagree_participants`). Tapi di beberapa UI component, belum diverifikasi apakah kedua signal ini ditampilkan secara terpisah.

### §06: Belief Creation
✅ A. AI detected: `/api/beliefs/extract` memanggil OpenRouter → Zod validation → insert ke `beliefs`.
✅ B. User created: `/api/beliefs/submit` ada, menangani submission langsung.

### §07: Creator Confirmation
🔴 **EIP-712 domain/type MISMATCH** antara frontend dan backend (lihat BUG-13). Signature verification akan selalu gagal.
✅ Flow konseptual benar: connect → sign → verify → badge.

### §08: Market Status (6 status)
⚠️ **Partial**. Status di DB (`DbMarketStatus`) tidak lengkap sesuai brief:
- Brief: `DETECTED → OPEN → CONFIRMED → CLOSED → RESOLVED → SETTLED`
- Kode: `active | cancelled | OPEN | CLOSED | RESOLVED | SETTLED` — ada `active` (lowercase) yang bukan dari brief, `DETECTED` dan `CONFIRMED` tidak ada di `DbMarketStatus` (ada di `DbBeliefStatus` saja).

### §09: Market Rules (7 aturan)
✅ Outcome objektif, deadline fixed, resolution condition immutable (on-chain).
✅ VOID mechanism ada di `OmenMarket.sol`.
⚠️ Aturan 7: "Gak ada manual admin settlement" — tapi ada `/api/markets/[id]/resolve` POST yang memungkinkan admin resolve manual tanpa oracle check. Ini bisa saja dimaksudkan untuk emergency, tapi perlu dicatat.

### §10: Price Oracle Architecture
✅ Chainlink → Smart Contract → Resolution Engine diimplementasi.
🔴 Feed addresses untuk Robinhood Chain **menggunakan Sepolia addresses** (BUG-08). Belum diverifikasi per §2.2.

### §11: Robinhood Market Data
⚠️ **Tidak ada implementasi** market data API Robinhood. Env var `ROBINHOOD_MARKET_DATA_API_KEY` didefinisikan di brief tapi **tidak ada di `.env.example`** dan tidak ada kode yang menggunakannya. Brief menyebutkan ini opsional untuk V1 ("cuma buat display"), jadi tidak kritis.

### §12: Pool Asset
✅ ETH sebagai pool currency — benar, semua deposit dalam ETH native.

### §13–14: Testnet Strategy & Network Configuration
✅ Dual testnet config (Sepolia + Robinhood Chain 46630) ada di `constants.ts` dan `wagmi.ts`.
✅ Chain ID, RPC URL, Explorer URL sesuai.

### §15–18: Smart Contract Architecture
✅ `OmenFactory.sol` dan `OmenMarket.sol` ada — sesuai brief.
🔴 Tapi `PredictionMarket.sol` (kontrak lama) masih ada dan **masih digunakan** oleh frontend hooks. Dua arsitektur kontrak bertentangan (BUG-01).
✅ Factory pattern: `createMarket` → deploy `OmenMarket` child.
✅ Belief hash, source hash, resolution hash on-chain.
✅ Events: `MarketCreated, PositionTaken, MarketResolved, PayoutClaimed, MarketVoided` — sesuai §15.
✅ Claim model: user klaim sendiri via `claimPayout()`.

### §19–21: Wallet & Admin
✅ wagmi + viem, support injected wallets (MetaMask, Rabby, Coinbase Wallet, Phantom).
✅ Tidak custody private key user.
✅ Admin roles terpisah di `OmenFactory.sol`: `DEFAULT_ADMIN_ROLE`, `MARKET_CREATOR_ROLE`, `RESOLVER_ROLE`.
⚠️ Brief menyebutkan `DEPLOYER, ADMIN, RESOLVER, TREASURY` — ada 3 dari 4 (TREASURY tidak ada).

### §22: Backend/Stack
✅ Next.js App Router, TypeScript, Tailwind, shadcn/ui.
✅ Supabase, PostgreSQL, viem, wagmi, OpenZeppelin, Foundry.
✅ AI: OpenRouter dengan model abstraction.

### §23: Database (11 tabel)
| Tabel Brief | Ada di DB Types? | Ada di API? |
|---|---|---|
| `users` | ✅ | ✅ |
| `beliefs` | ✅ | ✅ |
| `belief_sources` | ✅ | ✅ |
| `markets` | ✅ | ✅ |
| `market_positions` | ✅ | ✅ |
| `market_events` | ✅ | ✅ |
| `market_resolutions` | ✅ | ✅ |
| `market_settlements` | ✅ | ✅ |
| `creator_profiles` | ✅ | ✅ |
| `creator_confirmations` | ✅ | ✅ |
| `oracle_snapshots` | ✅ | ✅ |

⚠️ Ada tabel tambahan `bets` yang **tidak ada di brief §2.4** tapi ada di kode. Tabel ini **duplikat konseptual** dari `market_positions` — keduanya menyimpan data bet/posisi user. Ini melanggar DRY di layer data.

### §24: Creator Confirmation (EIP-712)
🔴 **Broken** — lihat BUG-13. Domain dan type mismatch antara frontend dan backend.

### §25: Market Metadata (Immutable Hash)
✅ `keccak256(metadata)` disimpan on-chain via `beliefHash`, `sourceHash`, `resolutionHash`.
✅ `metadata_hash` disimpan di DB.

### §26: Resolution Types V1 (3 jenis)
✅ `PRICE_ABOVE`, `PRICE_BELOW`, `RELATIVE_PERFORMANCE` — semua diimplementasi di `evaluateOracleCondition` dan `evaluateResolution`.

### §27: Tidak Didukung di V1
✅ Tidak ada subjective questions, multi-outcome, leveraged markets, dll.

### §28–35: UI & Pages
✅ Homepage, market page, market card, creator profile, discovery filter, activity feed — semua ada sebagai components/pages.
⚠️ Tidak diverifikasi secara visual dalam audit ini (audit kode saja).

### §36–37: Testnet Trust & Demo
⚠️ Kontrak perlu di-verify publik. Kode deployment sudah ada di `contracts/script/` tapi verifikasi aktual belum diaudit.

### §38–39: Security & Emergency
✅ `OmenMarket.sol`: `ReentrancyGuard`, `Pausable`, `onlyFactoryOrResolver`.
✅ Tidak ada admin withdrawal sembarangan.
✅ Resolution immutable setelah set.
✅ `hasClaimed` mapping mencegah double-claim.
🔴 `PredictionMarket.sol` **tidak memiliki Pausable** — hanya `ReentrancyGuard`.

### §40: Indexing
✅ Supabase + API-based event recording (bukan The Graph). Sesuai brief.

### §41: Frontend Architecture
✅ Struktur folder sesuai: `app/`, `components/`, `lib/`, `contracts/`, `hooks/`.
⚠️ Brief menyebutkan `lib/wallet/`, `lib/api/` — ini tidak ada sebagai subdirectori terpisah.

### §42–43: Stack & Env
✅ Stack sesuai.
⚠️ Env vars di `.env.example` **tidak lengkap** vs brief §2.1:
- Hilang: `NEXT_PUBLIC_CHAIN_ENV`, `NEXT_PUBLIC_ETH_SEPOLIA_RPC`, `NEXT_PUBLIC_ROBINHOOD_TESTNET_RPC`, `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA`, `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD`, `NEXT_PUBLIC_CHAINLINK_*`, `ROBINHOOD_MARKET_DATA_API_KEY`, `DEPLOYER_PRIVATE_KEY`.
- Ada tapi beda nama: `AI_API_KEY` (brief) vs `OPENROUTER_API_KEY` (kode).

### §44: Development Phases
- **P01 Smart Contract Core**: ✅ Done (deploy verified).
- **P02 Wallet + Frontend**: ✅ Done.
- **P03 Oracle**: ✅ Done (Chainlink integration).
- **P04 Belief Engine**: ✅ Done (OpenRouter AI extraction).
- **P05 Creator Confirmation**: 🔴 **Broken** (EIP-712 mismatch).
- **P06 Robinhood Chain Testnet**: ⚠️ Konfigurasi ada, tapi Chainlink feeds belum diverifikasi.

### §45: V1 Definition of Done
⚠️ **Partial**: Connect wallet → buka market → pilih AGREE/DISAGREE → sign tx → lihat posisi → market resolve → klaim payout — **secara kode alur ini ada**, tapi karena BUG-01 (dual contract architecture) dan BUG-13 (EIP-712 broken), **full cycle belum bisa berjalan end-to-end tanpa error**.

### §46: Trust Checklist
| Check | Status |
|---|---|
| Contract source verified | ⚠️ Perlu konfirmasi deployment |
| No admin custody | ✅ |
| Resolution immutable | ✅ |
| Deadline immutable | ✅ |
| Oracle source immutable | ✅ |
| Reentrancy protection | ✅ |
| Safe ETH transfer | ✅ |
| Pause mechanism tested | ⚠️ Ada di OmenMarket, tidak ada di PredictionMarket |
| Refund/VOID tested | ✅ Di OmenMarket |
| No double-claim | ✅ |
| No double-resolve | ✅ |

### §47: Test Cases
✅ 349 unit tests passing (66 files).
⚠️ Test coverage belum diaudit secara mendalam, tapi test suites mencakup: API routes, hooks, components, admin flows, E2E belief-market cycle.

### §48: V1 Product Limit
✅ Core product (market engine, settlement, wallet, oracle, UI) bisa berjalan tanpa AI detection.

### §51: Sumber Belief — Input Manual
✅ Form submit belief → `/api/beliefs/extract` → OpenRouter → Zod → insert.
✅ Alur step-by-step sesuai.

### §2.5: EIP-712 Creator Confirmation
🔴 **Broken** — lihat BUG-13.

### §2.7: Checklist Keamanan
| Requirement | Status |
|---|---|
| ReentrancyGuard di claim/resolve | ✅ (OmenMarket) / ✅ (PredictionMarket) |
| No arbitrary admin withdrawal | ✅ |
| Resolution & deadline immutable | ✅ |
| No double-claim | ✅ (`hasClaimed` mapping) |
| No double-resolve | ✅ (state machine check) |
| Pausable emergency | ✅ (OmenMarket) / 🔴 (PredictionMarket) |

---

## BAGIAN 4 — Integrasi DB & On-Chain, Mock/Dummy Data

### DB Integration
✅ Semua 12 tabel DB (11 dari brief + `bets`) diintegrasikan via Supabase client.
✅ Semua API routes menggunakan `getSupabaseAdminClient()` atau `getSupabaseClient()`.
✅ Tidak ada hardcoded data di production code.

### On-Chain Integration
✅ `factory-client.ts` → `createOnChainMarket()` deploy OmenMarket via OmenFactory.
✅ `resolution-engine.ts` → `resolveSingleMarket()` → writeContract ke OmenMarket.
✅ Frontend hooks (`usePlaceBet`, `useClaim`, `useClaimPayout`) memanggil contract via wagmi.
🔴 **Dual contract architecture** (BUG-01) membuat integrasi tidak konsisten.

### Mock/Dummy Data
✅ **Tidak ada mock data di production code** (src, lib, components, app, hooks).
✅ `MOCK_*` hanya ada di `tests/` directory — ini expected dan acceptable.
✅ File `mockOpenRouter.ts` sudah dihapus (confirmed dari session sebelumnya).
✅ `StatsOverview` menggunakan data dinamis dari Supabase.

---

## RINGKASAN PRIORITAS PERBAIKAN

| Prioritas | ID | Masalah |
|---|---|---|
| 🔴 P0 | BUG-01 | Pilih satu arsitektur contract (OmenFactory+OmenMarket atau PredictionMarket), hapus yang lain, sesuaikan semua hooks/ABI. |
| 🔴 P0 | BUG-13 | Fix EIP-712 domain/type mismatch antara frontend dan backend. |
| 🔴 P0 | BUG-08 | Verifikasi/konfigurasi Chainlink feed addresses per chain. |
| 🟡 P1 | BUG-03 | Implementasi atomic pool update (Supabase RPC/transaction). |
| 🟡 P1 | BUG-05 | Filter `snapshot_type` di oracle snapshot query. |
| 🟡 P1 | BUG-06 | Fix author-based profile lookup (handle vs wallet). |
| 🟡 P1 | BUG-07 | Fix `isCorrect` logic untuk reputation. |
| 🟡 P1 | BUG-11 | Set `protocolFeeBps` default ke 0 untuk testnet. |
| 🟡 P1 | BUG-14 | Standardisasi market status naming. |
| 🟢 P2 | DRY-* | Konsolidasi semua DRY violations. |
| 🟢 P2 | DRY-08,09 | Hapus inline `PREDICTION_MARKET_ABI`, gunakan JSON import. |
| 🟢 P2 | BUG-09 | Hapus definisi ulang `robinhoodChain`. |

---

*Laporan ini berisi temuan audit saja. Tidak ada perubahan kode yang dilakukan.*
