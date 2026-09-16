# OMEN V1 — Development Brief

**Status**: V1 Product + Technical Specification. **Kategori**: Social Belief Market. **Positioning**: *"OMEN turns social beliefs into tradable markets."*

**Mekanisme inti**: AI menemukan belief dari social internet → market langsung dibuka → user memilih AGREE atau DISAGREE → creator dapat mengkonfirmasi belief → market berjalan sampai deadline → oracle menentukan outcome → pool didistribusikan kepada pemenang → hasil menjadi bagian dari historical reputation.

## 01. Product Thesis
OMEN bukan prediction market biasa. Prediction market fokus ke "apa yang akan terjadi?"; OMEN fokus ke "apa yang dipercaya seseorang, dan apakah pasar setuju dengan keyakinan itu?" Core object-nya adalah **BELIEF**, yang punya: sumber asli, creator/author, statement, market condition, deadline, AGREE side, DISAGREE side, outcome, historical result.

## 02. V1 Principle
V1 harus sederhana. **Jangan bangun**: order book, AMM kompleks, leverage, perp, LP system, market making algorithm, social graph kompleks, token OMEN, DAO, creator revenue sharing kompleks. V1 cuma perlu buktiin: *"apakah orang mau mempertaruhkan modal berdasarkan belief orang lain?"* Core loop: `SOCIAL POST → AI BELIEF DETECTION → MARKET CREATION → AGREE/DISAGREE → SHARED POOL → DEADLINE → ORACLE RESOLUTION → WINNER DISTRIBUTION → REPUTATION`.

## 03. Market Model
Tiap market punya 2 sisi: AGREE / DISAGREE. Contoh: *"Will SOL outperform ETH in the next 30 days?"* Deadline 16 Okt 2026. Pool: AGREE 60 ETH, DISAGREE 40 ETH, total 100 ETH. User masuk ke salah satu sisi.

## 04. Pool Mechanism
V1 pakai **shared pari pool** — tanpa order book, tanpa dedicated LP. Semua dana masuk pool sesuai side. Kalau AGREE menang, AGREE winners dapat proporsional dari total pool (sama sebaliknya kalau DISAGREE menang). Formula payout: `user payout = (user winning stake / total winning pool) × distributable pool`. Protocol fee bisa diterapkan nanti; V1 sebaiknya configurable, default 0 di testnet.

## 05. Market Odds — Penting
Odds jangan jadi primitive utama. UI wajib tampilkan **CONSENSUS** (mis. 64% AGREE / 36% DISAGREE dari jumlah participant) **DAN** **CAPITAL** distribution terpisah (mis. 81% AGREE / 19% DISAGREE dari jumlah uang) — menciptakan social signal "apa yang orang bilang vs ke mana orang taruh modal".

## 06. Belief Creation
**A. AI detected**: AI menemukan belief dari social media, hasilkan JSON terstruktur (author, statement, subject, comparison, direction, timeframe, source, confidence). Market langsung dibuat, status `AI DETECTED`, creator confirmation TIDAK diperlukan buat buka market.
**B. User created**: user manual input belief + deadline + resolution condition; sistem validasi sebelum market dibuka.

## 07. Creator Confirmation
Ini **lapisan verifikasi sosial**, BUKAN permission buka market. Flow: AI detect → market opens → creator dapat notifikasi → creator confirm → market dapat badge verified. Setelah confirm, tampilan berubah dari "AI DETECTED" jadi "✓ CONFIRMED BY @handle". Creator TIDAK BISA mengubah market setelah dibuka — confirmation cuma ubah status verifikasi.

## 08. Market Status (6 status)
`DETECTED` (candidate belief, belum terima dana) → `OPEN` (aktif, bisa AGREE/DISAGREE) → `CONFIRMED` (creator konfirmasi, tetap OPEN) → `CLOSED` (deadline tercapai, no posisi baru) → `RESOLVED` (oracle tentukan: AGREE WON / DISAGREE WON / VOID) → `SETTLED` (dana terdistribusi).

## 09. Market Rules (7 aturan)
1. Outcome harus objektif (bukan "will crypto jadi bullish", tapi "will SOL outperform ETH by Oct 16"). 2. Deadline fixed, gak berubah setelah OPEN. 3. Resolution condition immutable setelah OPEN. 4. Resolution source (oracle, metric, timestamp) ditentukan SEBELUM market OPEN. 5. Kalau oracle gagal/kondisi gak bisa ditentukan → `VOID`, pool di-refund, jangan paksa ada winner. 6. Creator confirmation gak bisa mengubah market. 7. Gak ada manual admin settlement untuk market normal — admin cuma bisa emergency procedure yang transparan & tercatat.

## 10. Price Oracle Architecture
Untuk market berbasis harga: `Chainlink Oracle → Smart Contract → Resolution Engine`. Robinhood mendokumentasikan integrasi Chainlink & price feeds untuk Stock Tokens; Chainlink Data Streams juga tersedia buat data berlatensi rendah. V1 pakai **Standard Chainlink Price Feed** untuk market yang feednya tersedia. **Jangan** pakai frontend API sebagai sumber settlement — frontend API cuma buat display price/chart/preview/analytics. Settlement harus dari data yang bisa diverifikasi contract.

## 11. Robinhood Market Data
Robinhood sediakan API market data crypto (best bid/ask, pair kayak ETH-USD), pakai API key+signature+timestamp. Dipakai sebagai **OFFCHAIN market data** doang (current price, UI, chart, discovery, preview) — **JANGAN** jadi satu-satunya trust layer settlement. Arsitektur: Robinhood Market Data → Backend → UI (jalur tampilan), terpisah dari Chainlink Oracle → Smart Contract → Settlement (jalur settlement).

## 12. Pool Asset
V1 pakai **ETH** sebagai pool currency. Target deploy: Ethereum Sepolia + Robinhood Chain Testnet (native currency ETH, chain ID 46630). **Tidak perlu** bikin stablecoin sendiri, token OMEN, atau ERC20 khusus di V1.

## 13. Testnet Strategy
2 deployment testnet. **A. Ethereum Sepolia** — tujuan: public security demonstration, contract verification, wallet compatibility, public tx history, trusted deployment, developer testing gampang. **B. Robinhood Chain Testnet** — tujuan: native ecosystem integration, Robinhood Wallet testing, ETH pool testing, Robinhood oracle integration, public demonstration. Robinhood Chain resmi sediakan testnet, EVM compatible, tooling Ethereum standar, public explorer.

## 14. Network Configuration
Robinhood Chain Testnet — Chain ID `46630`, currency ETH, RPC `https://rpc.testnet.chain.robinhood.com`, Explorer `https://explorer.testnet.chain.robinhood.com`. Pakai RPC provider (bukan public RPC) kalau traffic udah tinggi — Robinhood rekomendasiin Alchemy.

## 15-18. Smart Contract Architecture
Minimal contract: `OmenFactory`, `OmenMarket` (resolver bisa module/library atau contract terpisah kalau perlu; `OmenResolver`/`OmenTreasury` opsional, gak wajib V1).
**OmenFactory** — tanggung jawab: create market, assign market ID, simpan metadata hash, configure resolver/deadline/pool token, emit `MarketCreated`. Contoh signature: `createMarket(bytes32 beliefHash, uint256 openTime, uint256 closeTime, ResolutionConfig calldata resolution)`. Belief text penuh **gak perlu** hidup di on-chain — cukup simpan `beliefHash`, `sourceHash`, `resolutionHash`; metadata lengkap di Supabase/IPFS, hash buat verifikasi integritas.
**OmenMarket** — tanggung jawab: terima deposit AGREE/DISAGREE, track posisi user, cegah deposit setelah deadline, close market, resolve outcome, hitung payout, izinkan claim. Events: `MarketCreated, PositionTaken, MarketClosed, MarketResolved, PayoutClaimed, MarketVoided`.
**Claim model**: JANGAN distribusi otomatis semua payout — market resolve → hitung winner amount → user klaim sendiri (hemat gas).

## 19-21. Wallet & Admin
**Wallet**: wagmi+viem, support MetaMask/Rabby/Coinbase Wallet/WalletConnect-compatible/Robinhood Wallet. **Tidak custody** private key user — user tanda tangan dari wallet sendiri.
**Signing**: semua aksi yang ubah state blockchain wajib wallet-signed (connect → pilih side → input amount → confirm wallet → sign → submit → tunggu konfirmasi → UI update). V1: no custodial wallet, no private key disimpan backend, no seed phrase, no backend signing atas nama user.
**Admin wallet**: HARUS terpisah dari user wallet. Pakai peran terpisah: `DEPLOYER, ADMIN, RESOLVER, TREASURY` — jangan 1 private key buat semua. Prefer multisig untuk produksi; buat testnet, 1 deployer key dedicated boleh. Robinhood eksplisit rekomendasiin jangan commit private key, pakai env var dengan throwaway deployer key buat testing.

## 22. Backend/Stack Ringkas
Frontend: Next.js App Router, TypeScript, Tailwind, shadcn/ui. Backend: Next.js Server Actions/Route Handlers, Supabase, PostgreSQL. Blockchain: viem, wagmi, OpenZeppelin, Foundry. AI: LLM provider abstraction (jangan tightly couple provider AI ke business logic).

## 23. Database
Tabel inti: `users, beliefs, belief_sources, markets, market_positions, market_events, market_resolutions, market_settlements, creator_profiles, creator_confirmations, oracle_snapshots`. (Skema detail 4 tabel dari brief + 7 tabel lainnya yang saya lengkapi ada di **Bagian 2, §4**.)

## 24. Creator Confirmation (Teknis)
Confirmation awalnya bisa **offchain signature** (hemat gas). Flow: creator connect wallet → OMEN tampilkan belief terdeteksi → klik CONFIRM → wallet sign pesan **EIP-712** → backend verifikasi signature → belief jadi `CONFIRMED`. Pesan berisi: pernyataan konfirmasi + belief text + market_id + timestamp. Signature = bukti kriptografis konfirmasi. Transaksi on-chain **opsional** di V1.

## 25. Market Metadata
Tiap market punya immutable metadata commitment: `{statement, deadline, resolution: {type, assetA, assetB, oracle}}` → hash `keccak256(metadata)` → simpan hash on-chain. Ini mencegah frontend/backend diam-diam ubah aturan market.

## 26. Resolution Types V1 (cuma 3)
1. **Price Above** ("Will ETH be above $5,000?"). 2. **Price Below**. 3. **Relative Performance** ("Will SOL outperform ETH?") — ini **signature market type** OMEN, formula `SOL return > ETH return`, pakai oracle price di titik START dan END.

## 27. Tidak Didukung di V1
Subjective questions, ambiguous language, manually judged outcomes, political markets, complex sports settlement, multi-outcome markets, conditional markets, leveraged markets, perpetuals, parimutuel odds manipulation, cross-chain settlement. Mulai dari financial market yang objektif terukur aja.

## 28. UI Direction
Referensi mental model: **Kalshi** (information hierarchy, market card, simple outcome selection, probability display, clean trading UI) dan **Polymarket** (market discovery, social context, volume, trader activity, information density) — **jangan clone UI mereka**. OMEN butuh lapisan khas: **Social Belief First** — market harus terasa: `PERSON → BELIEF → MARKET → CROWD → OUTCOME`.

## 29-35. Halaman & UI Detail
**Homepage**: nav (Markets, Beliefs, Creators, Activity, Connect Wallet), hero *"THE INTERNET IS FULL OF OPINIONS. OMEN GIVES THEM A MARKET."*, section "Trending Beliefs" isi market card.
**Market page** (desktop): panel Belief (statement, badge confirmed, deadline) + panel Take Position (AGREE/DISAGREE button, input amount) + panel Price/Market Data (chart) + panel Source (link post asli) + panel Resolution (oracle, deadline).
**Market card** wajib komunikasikan 5 hal sekaligus: WHO, WHAT, WHEN, CONSENSUS, MONEY.
**Creator profile**: handle, jumlah confirmed beliefs, resolved, correct, % akurasi; section Active/Resolved Beliefs, Record, Categories — tiap belief link balik ke sumber asli.
**Discovery feed**: tab Trending/Newest/Ending Soon/Most Volume/Confirmed (For You/Following = future, JANGAN bikin algoritma personalisasi di V1).
**Activity**: feed publik aktivitas on-chain (wallet, action, belief, amount, waktu) — bikin OMEN kelihatan "hidup" secara ekonomi.
**Onchain transparency**: UI wajib expose Contract, Market ID, Chain, Transaction, Oracle, Resolution — link ke explorer.

## 36-37. Testnet Trust & Demo
Sebelum public launch: deploy ke Sepolia dulu (verify contract publik, publish address+ABI+source+deployment tx+test market+oracle config), BARU deploy set sama ke Robinhood Chain Testnet (verify di Blockscout). Demo publik harus dukung siklus lengkap: create belief → market → 2 user beda sisi → close → resolve → claim → **verifiable independen** oleh pengunjung manapun di explorer.

## 38-39. Security & Emergency
Pakai OpenZeppelin: reentrancy protection, access control, safe ETH transfer, pausable emergency, checks-effects-interactions. Contract **TIDAK BOLEH**: admin withdrawal sembarangan, modifikasi balance tersembunyi, resolution berubah setelah open, pemilihan winner sembarangan, custody private key user. Admin boleh pause deposit baru kalau ada vulnerability kritis, tapi PAUSE **tidak boleh** bikin admin bisa curi dana user — mekanisme emergency withdrawal/refund harus didefinisikan eksplisit, semua fungsi privileged emit event.

## 40. Indexing
V1 cukup pakai Supabase + RPC event listener (dengerin `MarketCreated, PositionTaken, MarketClosed, MarketResolved, PayoutClaimed`). The Graph/dedicated indexer itu urusan nanti, jangan ditambah prematur.

## 41. Frontend Architecture (struktur folder)
```text
app/ (page, markets/, market/[id]/, beliefs/, belief/[id]/, creators/, creator/[address]/, activity/, docs/)
components/ (market-card/, market-chart/, position-panel/, belief-card/, creator-card/, wallet/, confirmation/, activity/)
lib/ (blockchain/, oracle/, market/, belief/, wallet/, api/)
contracts/ (abi/, addresses/)
hooks/ (useMarket, usePosition, useCreateMarket, useResolveMarket, useClaim)
```

## 42-43. Stack & Env (ringkas, detail lengkap di §51)
Frontend Next.js+TS+Tailwind+shadcn. Web3: viem, wagmi, WalletConnect, OpenZeppelin, Foundry. DB: Supabase/PostgreSQL. AI: LLM provider abstraction. RPC: Alchemy preferred. Oracle: Chainlink. Storage: Supabase (+IPFS opsional). Env var never expose private key lewat `NEXT_PUBLIC_*`.

## 44. Development Phases (6 fase)
**P01** Smart Contract Core (OmenFactory+OmenMarket: create/deposit/close/resolve/claim, deploy+verify Sepolia). **P02** Wallet+Frontend (connect, market list/page, AGREE/DISAGREE, claim, explorer link). **P03** Oracle (ETH/USD, BTC/USD, SOL/USD sesuai feed yang verified tersedia; Start/End Price, Relative Performance). **P04** Belief Engine (social source → AI extraction → structured belief → validation → market creation; AI **tidak boleh** deploy market sembarangan tanpa validasi). **P05** Creator Confirmation (connect → sign EIP-712 → verify → badge). **P06** Robinhood Chain Testnet (deploy ulang ke chain 46630, verify publik, tes ulang full siklus).

## 45. V1 Definition of Done
User baru bisa: visit OMEN → connect wallet → buka live belief market → baca sumber asli → lihat status confirm → pilih AGREE/DISAGREE → sign tx → lihat posisi on-chain → tunggu deadline → market resolve via oracle → menang → klaim payout → verifikasi tx di explorer. **Tidak ada step yang butuh campur tangan admin** di siklus normal.

## 46. Trust Checklist
Kontrak source verified, no admin custody, resolution immutable, deadline immutable, oracle source immutable, reentrancy protection, safe ETH transfer, pause mechanism tested, refund/VOID mechanism tested, no double-claim, no double-resolve, position accounting tested, edge case tested, wallet signing tested, explorer verification tested.

## 47. Test Cases (minimum)
Create market; tolak market invalid; tolak deposit sebelum open; deposit selama open jalan; tolak deposit setelah close; AGREE/DISAGREE deposit jalan; tolak resolve sebelum deadline; resolve setelah deadline jalan; winner benar terima payout; loser gak bisa klaim; winner gak bisa klaim dobel; VOID market refund benar; zero pool & minimum pool tertangani; admin gak bisa curi pool; market paused berperilaku benar.

## 48. V1 Product Limit (Penting)
**Jangan** bangun sistem ingest social internet penuh sebelum market engine jalan. Prioritas: `MARKET ENGINE → ONCHAIN SETTLEMENT → WALLET → ORACLE → UI → AI BELIEF DETECTION → CREATOR CONFIRMATION`. **Core product harus tetap jalan walau AI detection sementara dimatikan.**

## 49. Final Technical Principle
OMEN **bukan** "AI app dengan prediction market nempel", tapi **"Market Protocol dengan AI-powered belief discovery layer + social reputation layer"**. Layer settlement finansial harus deterministik; layer AI boleh probabilistik. Pembagian: **AI = discovery, Smart Contract = uang, Oracle = sumber kebenaran, Wallet = otoritas user, Social layer = distribusi, Reputation = memori.** Pemisahan ini kritis buat trust.

## 50.
*"Build a trustless two sided ETH belief market where AI discovers beliefs from social media, markets open automatically, users take AGREE or DISAGREE positions, creator confirmation adds verified social proof, and objective oracle data determines the winner and distributes the pool onchain."*

## Referensi Resmi
Dokumentasi developer Robinhood Chain jadi source of truth network config/deploy/RPC/explorer/ekosistem. Robinhood Chain EVM-compatible, testnet chain ID 46630, ETH native, tooling Ethereum standar. Chainlink didokumentasikan sebagai oracle partner (termasuk pricing on-chain buat Stock Tokens). Canonical bridge pakai Ethereum sebagai L1 security layer via Arbitrum canonical bridge. **Chain Terms Robinhood eksplisit: testnet buat testing, token testnet gak ada nilai moneter** — jadi V1 ini wajib tetap eksperimen testnet sampai model legal/regulasi/operasional buat real-value market dibikin terpisah.

---

## 51. Sumber "Belief" untuk V1: Input Manual

Belief tetap berstatus "AI DETECTED" tapi sumbernya **manual-paste**, bukan integrasi/scraping otomatis ke API sosial media manapun.

**Ditempatkan di**: halaman `/create` atau modal "Submit Belief" (tambahan CTA di navbar homepage, di samping "Connect Wallet").

**Alur step-by-step**:
1. User/admin isi form: **teks asli** (copy-paste dari post apapun), **link sumber**, **handle/nama author**.
2. Submit ke `/api/beliefs/extract` (POST): `{ raw_text, source_url, author_handle }`.
3. Backend panggil **OpenRouter** (model gratis) — prompt minta LLM **cuma struktur-in** teks yang dikasih (bukan cari sendiri) jadi JSON sesuai §06A: `{ author, statement, subject, comparison, direction, timeframe, source, confidence }`. `confidence` di sini = seberapa yakin LLM berhasil ekstrak struktur jelas dari teks, bukan soal kebenaran prediksinya.
4. Validasi output pakai **Zod** — field wajib (subject, comparison, timeframe) gak lengkap → tolak, minta user perbaiki.
5. Valid → insert ke `beliefs` (`status: 'DETECTED'`, `source_platform` bebas diisi apa aja, gak dibatasi ke satu platform).
6. Trigger `OmenFactory.createMarket` sesuai alur §07.

**Output**: 1 row baru di `beliefs` (status `DETECTED`) + 1 market baru ter-deploy on-chain.

## 2.1 Environment Variables Lengkap

```bash
NEXT_PUBLIC_CHAIN_ENV=testnet

NEXT_PUBLIC_ETH_SEPOLIA_RPC=
NEXT_PUBLIC_ROBINHOOD_TESTNET_RPC=https://rpc.testnet.chain.robinhood.com
NEXT_PUBLIC_ROBINHOOD_CHAIN_ID=46630
NEXT_PUBLIC_ROBINHOOD_EXPLORER=https://explorer.testnet.chain.robinhood.com

NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA=
NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD=

NEXT_PUBLIC_CHAINLINK_ETH_USD_FEED=
NEXT_PUBLIC_CHAINLINK_SOL_USD_FEED=      # perlu diverifikasi, lihat 2.2


AI_API_KEY=                              # OpenRouter
AI_MODEL=

ADMIN_PRIVATE_KEY=                       # SERVER-SIDE ONLY
DEPLOYER_PRIVATE_KEY=                    # SERVER-SIDE ONLY, dipakai sekali di awal

ROBINHOOD_MARKET_DATA_API_KEY=           # opsional, cuma buat display
ROBINHOOD_MARKET_DATA_SECRET=
```
⚠️ Private key TIDAK BOLEH pernah masuk variable `NEXT_PUBLIC_*`.

## 2.2 Verifikasi Chainlink Feed (Wajib Sebelum Phase 03)

Chainlink terkonfirmasi jadi oracle resmi Robinhood Chain (mainnet & testnet, dari block zero), tapi feed yang terkonfirmasi publik itu untuk **tokenized equity** (NVDA, GOOG, dst), bukan pasti buat pair crypto (SOL/USD, ETH/USD).

**Sebelum mulai Phase 03**: cek https://docs.chain.link/data-feeds untuk network Robinhood Chain — pastikan feed SOL/USD & ETH/USD ada. Kalau belum ada: mulai dari Resolution Type 1/2 (Price Above/Below) pakai feed yang beneran tersedia, tunda Type 3 (Relative Performance) sampai feed crypto pair dikonfirmasi — atau pakai feed Ethereum Sepolia dulu (lebih lengkap) untuk Deployment A.

## 2.3 RPC Provider

Cek dashboard Alchemy — apakah network "Robinhood Chain" udah terdaftar (chain baru, gak semua provider otomatis nambahin cepat). Kalau belum ada: fallback ke RPC publik resmi `https://rpc.testnet.chain.robinhood.com`. Untuk Sepolia, Alchemy/Infura free tier udah pasti support.

## 2.4 Skema Database Lengkap (11 Tabel)

```sql
beliefs (
  id UUID PK, author TEXT, statement TEXT NOT NULL, source_url TEXT,
  source_platform TEXT DEFAULT 'manual', source_timestamp TIMESTAMP,
  ai_confidence NUMERIC,
  status TEXT CHECK (status IN ('DETECTED','OPEN','CONFIRMED','CLOSED','RESOLVED','SETTLED')),
  created_at TIMESTAMP DEFAULT now()
)

belief_sources (
  id UUID PK, belief_id UUID FK -> beliefs.id, raw_text TEXT NOT NULL,
  submitted_by_wallet TEXT, created_at TIMESTAMP DEFAULT now()
)

markets (
  id UUID PK, belief_id UUID FK -> beliefs.id, contract_address TEXT NOT NULL,
  chain_id INTEGER NOT NULL, agree_pool NUMERIC DEFAULT 0, disagree_pool NUMERIC DEFAULT 0,
  open_time TIMESTAMP NOT NULL, close_time TIMESTAMP NOT NULL,
  resolution_type TEXT CHECK (resolution_type IN ('PRICE_ABOVE','PRICE_BELOW','RELATIVE_PERFORMANCE')),
  resolution_config JSONB, metadata_hash TEXT, status TEXT,
  winner TEXT CHECK (winner IN ('AGREE','DISAGREE','VOID', NULL)),
  created_at TIMESTAMP DEFAULT now()
)

market_positions (
  id UUID PK, market_id UUID FK -> markets.id, wallet_address TEXT NOT NULL,
  side TEXT CHECK (side IN ('AGREE','DISAGREE')), amount NUMERIC NOT NULL,
  claimed BOOLEAN DEFAULT false, tx_hash TEXT UNIQUE NOT NULL, created_at TIMESTAMP DEFAULT now()
)

market_events (
  id UUID PK, market_id UUID FK -> markets.id,
  event_type TEXT, -- MarketCreated|PositionTaken|MarketClosed|MarketResolved|PayoutClaimed|MarketVoided
  wallet_address TEXT, amount NUMERIC, tx_hash TEXT UNIQUE NOT NULL,
  block_number INTEGER, created_at TIMESTAMP DEFAULT now()
)

market_resolutions (
  id UUID PK, market_id UUID FK -> markets.id, oracle_source TEXT DEFAULT 'chainlink',
  start_price NUMERIC, end_price NUMERIC,
  resolved_outcome TEXT CHECK (resolved_outcome IN ('AGREE','DISAGREE','VOID')),
  resolution_tx_hash TEXT, resolved_at TIMESTAMP DEFAULT now()
)

market_settlements (
  id UUID PK, market_id UUID FK -> markets.id, total_pool NUMERIC,
  distributable_pool NUMERIC, protocol_fee NUMERIC DEFAULT 0, settled_at TIMESTAMP DEFAULT now()
)

creator_profiles (
  id UUID PK, wallet_address TEXT UNIQUE NOT NULL, handle TEXT,
  confirmed_beliefs_count INTEGER DEFAULT 0, resolved_count INTEGER DEFAULT 0,
  correct_count INTEGER DEFAULT 0, created_at TIMESTAMP DEFAULT now()
)

creator_confirmations (
  id UUID PK, belief_id UUID FK -> beliefs.id, creator_wallet TEXT NOT NULL,
  confirmed_at TIMESTAMP DEFAULT now(), signature TEXT NOT NULL, tx_hash TEXT
)

oracle_snapshots (
  id UUID PK, market_id UUID FK -> markets.id,
  source TEXT CHECK (source IN ('chainlink','robinhood_market_data')),
  asset TEXT, price NUMERIC, snapshot_type TEXT CHECK (snapshot_type IN ('START','END','DISPLAY')),
  recorded_at TIMESTAMP DEFAULT now()
)

users (
  id UUID PK, wallet_address TEXT UNIQUE NOT NULL, created_at TIMESTAMP DEFAULT now()
)
```

## 2.5 EIP-712 Creator Confirmation — Detail Implementasi

1. Frontend generate typed data EIP-712 (`domain: {name:"OMEN", version:"1", chainId}`, `message: {belief, market_id, timestamp}`).
2. Panggil `signTypedData` dari wagmi (bukan `personal_sign` — EIP-712 lebih aman & jelas ditampilkan wallet).
3. Kirim signature ke `/api/beliefs/:id/confirm`, backend verifikasi pakai `viem`'s `verifyTypedData`, cocokkan signer address ke creator terdaftar.
4. Update `beliefs.status` jadi `CONFIRMED`, insert row ke `creator_confirmations`.

## 2.6 Deployment Checklist (Dual Testnet)

1. Deploy `OmenFactory`+`OmenMarket` ke **Sepolia**, verify di Etherscan, publish address+ABI+source.
2. Tes 1 siklus penuh di Sepolia (create → market → 2 wallet beda sisi → close → resolve → claim → cek explorer).
3. Deploy ulang set kontrak sama ke **Robinhood Chain testnet** (46630), verify di Blockscout.
4. Ulangi tes siklus penuh di Robinhood Chain testnet.
5. Frontend baca `NEXT_PUBLIC_CHAIN_ENV` buat default chain, user tetap bisa switch manual.

## 2.7 Checklist Keamanan (Konkret)

| Requirement | Cara Konkret |
|---|---|
| Reentrancy protection | `ReentrancyGuard` OpenZeppelin di semua fungsi `claim`/`resolve` |
| No arbitrary admin withdrawal | Gak ada fungsi withdraw admin bebas — cuma emergency refund proporsional fixed-formula |
| Resolution & deadline immutable | `closeTime`/`resolutionConfig` di-set sekali di `createMarket`, tanpa setter |
| No double-claim | Mapping `hasClaimed[marketId][wallet]`, cek sebelum transfer |
| No double-resolve | State machine: `resolve()` cuma jalan kalau status `CLOSED`, langsung ubah `RESOLVED` di awal (checks-effects-interactions) |
| Pausable emergency | `Pausable` OpenZeppelin, cuma blokir deposit baru, TIDAK blokir claim yang udah resolve |

## 2.8 Catatan Biaya / Free-Tier

- AI: OpenRouter model gratis (cuma buat structuring input manual)
- RPC Sepolia: Alchemy/Infura free tier
- RPC Robinhood testnet: RPC publik resmi, gratis
- Chainlink: baca on-chain, gratis (bayar gas testnet doang)
- Test ETH: faucet Sepolia publik + faucet Robinhood Chain testnet (cek docs.robinhood.com/chain)
