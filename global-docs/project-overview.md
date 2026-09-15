# Project 3 — Points/Quest Farming + Prediction Market Dashboard

## 1. Ringkasan
Satu dashboard yang menggabungkan dua utility dalam satu token/ekosistem: **points/quest farming** (user dapat poin dari menyelesaikan quest/aktivitas harian, bukan sekadar lock token) dan **prediction market** bertema crypto/meme (tebak harga, tebak trend, tebak hasil launch token lain). Poin dipakai untuk leaderboard, dan berpotensi jadi dasar reward/airdrop di masa depan.

## 2. Target User
User yang suka "farming" aktivitas buat kumpulin poin/potensi airdrop, dan trader yang suka gamble/taruhan on-chain (prediction market bettor).

## 3. Tech Stack
- **Frontend**: Next.js 14+, TypeScript, Tailwind CSS
- **Smart Contract**: 2 contract utama —
  1. `PointsEngine.sol` (mencatat/verifikasi poin per wallet dari aksi on-chain tertentu — opsional bisa full off-chain di DB kalau poin tidak perlu tercatat di blockchain untuk MVP, lebih simpel & murah gas)
  2. `PredictionMarket.sol` (create market sederhana dengan resolusi manual/oracle admin dulu untuk MVP — bukan oracle terdesentralisasi penuh, supaya realistis dikerjakan 1 dev dalam sebulan)
- **Wallet Connect**: Phantom Wallet (EVM mode) via `wagmi` + `viem`
- **Database**: Neon atau Supabase — untuk cache data market (judul, deadline, status), poin, dan daftar quest
- **Hosting**: Vercel

## 4. Arsitektur Singkat
```
User --(connect Phantom)--> Frontend
Frontend --(selesaikan quest)--> API Route --(validasi aksi)--> DB (catat poin)
Frontend --(create/bet/claim market)--> PredictionMarket.sol (on-chain)
Backend API --(index event on-chain)--> DB (cache market list, leaderboard poin)
Admin Panel --(resolve market manual / tambah quest baru)--> DB + PredictionMarket.sol.resolve()
```

## 5. Fitur MVP
1. **Landing/Overview** — total user aktif, jumlah poin terdistribusi, jumlah market aktif, link CA token.
2. **Connect Wallet Phantom (EVM)**.
3. **Daily Check-in** — user klaim poin harian (1x per 24 jam per wallet), streak counter (opsional bonus kalau check-in berturut-turut).
4. **Quest List** — daftar tugas sederhana yang kasih poin kalau diselesaikan (contoh: connect wallet pertama kali, ikut 1 prediction market, follow akun X project, invite teman via referral code). Verifikasi quest cukup sederhana (cek dari DB/aksi di app, tidak perlu semua on-chain).
5. **Points Leaderboard** — ranking wallet berdasarkan total poin.
6. **Prediction Market List** — daftar market aktif (mis. "Apakah token X akan naik >20% minggu ini?"), tiap market punya 2 opsi (Yes/No) + total pool tiap sisi.
7. **Betting Flow** — user pilih opsi, input jumlah token, konfirmasi transaksi on-chain.
8. **Klaim Kemenangan** — setelah market di-resolve admin, user yang menang bisa klaim payout proporsional. Ikut prediction market juga menambah poin (terlepas menang/kalah).
9. **Admin Panel sederhana** (halaman terpisah, akses dibatasi wallet admin) — buat/nonaktifkan quest, buat market baru, resolve market (input hasil Yes/No).

## 6. Fitur Fase 2
- Referral system dengan multiplier poin (ajak teman → poin bertambah untuk keduanya).
- Oracle otomatis (integrasi price feed on-chain) untuk market berbasis harga, mengurangi ketergantungan resolusi manual.
- Leaderboard "prediktor terbaik" (win rate tertinggi) terpisah dari leaderboard poin umum.
- Konversi poin ke reward token/airdrop di masa depan (mekanismenya menyusul, tidak perlu dikerjakan sekarang).
- Notifikasi market akan segera ditutup / quest baru tersedia.

## 7. User Flow — Points/Quest
1. Connect wallet → halaman "Quests & Points".
2. User lihat daftar quest aktif + status selesai/belum.
3. User selesaikan aksi (mis. klik "Daily Check-in", atau ikut prediction market) → sistem catat poin ke DB.
4. Leaderboard poin update, user bisa lihat rank sendiri.

## 7b. User Flow — Prediction Market
1. User buka tab "Predictions" → lihat daftar market aktif dengan pool masing-masing sisi.
2. Pilih market → pilih Yes/No → input jumlah taruhan → confirm transaksi.
3. Setelah deadline lewat, admin resolve market via admin panel.
4. User yang menang buka halaman "My Bets" → klik Claim → dana masuk ke wallet. Poin ikut ditambahkan otomatis setelah user berpartisipasi.

## 8. Skema Database
```sql
-- users
users (
  id UUID PK,
  wallet_address TEXT UNIQUE NOT NULL,
  total_points NUMERIC DEFAULT 0,
  last_checkin_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT now()
)

-- quests
quests (
  id UUID PK,
  title TEXT NOT NULL,
  description TEXT,
  points_reward NUMERIC NOT NULL,
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT now()
)

-- points_events (log setiap poin masuk, sumbernya dari mana)
points_events (
  id UUID PK,
  wallet_address TEXT NOT NULL,
  quest_id UUID FK -> quests.id NULL, -- null kalau sumbernya bukan quest (misal dari ikut market)
  source TEXT NOT NULL, -- 'daily_checkin','quest','prediction_market','referral'
  points NUMERIC NOT NULL,
  created_at TIMESTAMP DEFAULT now()
)

-- markets
markets (
  id UUID PK,
  contract_market_id INTEGER UNIQUE NOT NULL, -- id di smart contract
  title TEXT NOT NULL,
  description TEXT,
  deadline TIMESTAMP NOT NULL,
  status TEXT CHECK (status IN ('active','resolved_yes','resolved_no','cancelled')) DEFAULT 'active',
  created_at TIMESTAMP DEFAULT now()
)

-- bets
bets (
  id UUID PK,
  market_id UUID FK -> markets.id,
  wallet_address TEXT NOT NULL,
  side TEXT CHECK (side IN ('yes','no')),
  amount NUMERIC NOT NULL,
  claimed BOOLEAN DEFAULT false,
  tx_hash TEXT UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT now()
)
```

## 9. Daftar API Endpoint
| Method | Path | Fungsi |
|---|---|---|
| POST | `/api/wallet/connect` | Upsert wallet user |
| POST | `/api/checkin` | Klaim poin daily check-in |
| GET | `/api/quests` | List quest aktif + status per wallet |
| POST | `/api/quests/:id/complete` | Tandai quest selesai, tambah poin |
| GET | `/api/leaderboard/points` | Ranking wallet berdasarkan total poin |
| GET | `/api/markets` | List market aktif/selesai |
| POST | `/api/markets` | (admin only) buat market baru di DB setelah dibuat di contract |
| POST | `/api/markets/:id/resolve` | (admin only) update status market setelah resolve on-chain |
| GET | `/api/bets?wallet=` | Riwayat taruhan user |
| POST | `/api/bets/index` | Index event Bet dari blockchain (dipanggil listener/indexer), sekaligus tambah poin partisipasi |

## 10. Wallet & Keamanan
- Aksi finansial (bet, claim) **wajib** transaksi on-chain langsung dari wallet user — backend hanya mencatat/cache, tidak pernah menyimpan/mengelola dana user.
- Poin cukup disimpan di database (off-chain) untuk MVP — tidak perlu smart contract khusus poin kecuali nanti dikonversi ke reward on-chain (fase 2).
- Admin panel wajib dibatasi: cek `wallet_address` yang connect harus cocok dengan `ADMIN_WALLET_ADDRESS` di env sebelum mengizinkan create/resolve market atau quest.
- Untuk MVP, resolusi market manual oleh admin cukup dilengkapi disclaimer transparansi (sumber data resolusi dicatat di deskripsi market).

## 11. Smart Contract (scope kerja dev)
- `PredictionMarket.sol`: fungsi `createMarket(...)`, `placeBet(uint marketId, bool side, uint amount)`, `resolveMarket(uint marketId, bool result)` (onlyOwner), `claim(uint marketId)`.
- Poin (`PointsEngine`) untuk MVP **tidak wajib on-chain** — cukup logic di backend/DB. Kalau nanti dibutuhkan on-chain (misal untuk transparansi penuh), itu masuk fase 2.
- Deploy & test `PredictionMarket.sol` di testnet dulu sebelum mainnet. Bukan scope: audit formal / oracle terdesentralisasi (dicatat sebagai roadmap fase 2).

## 12. Wajib Testnet Dulu Sebelum Mainnet
- **Semua development & testing smart contract `PredictionMarket.sol` WAJIB dilakukan di testnet dulu.** Jangan deploy langsung ke mainnet Robinhood Chain.
- Cek dulu apakah Robinhood Chain punya testnet resmi di docs.robinhood.com. Kalau belum tersedia/tidak jelas, karena Robinhood Chain berbasis Arbitrum Orbit, pakai **Arbitrum Sepolia** sebagai testnet pengganti untuk development awal.
- Faucet test ETH gratis untuk Arbitrum Sepolia:
  - Alchemy Faucet — https://www.alchemy.com/faucets/arbitrum-sepolia (0.1 ETH/24 jam, tanpa signup)
  - QuickNode Faucet — https://faucet.quicknode.com/arbitrum/sepolia
  - LearnWeb3 Faucet — https://learnweb3.io/faucets/arbitrum_sepolia/ (login GitHub)
- Baru pindah ke mainnet Robinhood Chain setelah flow bet/resolve/claim lolos QA penuh di testnet.

## 13. Deployment ke Vercel
1. Deploy `PredictionMarket.sol` ke Robinhood Chain (testnet → mainnet), simpan address & ABI.
2. Push frontend ke GitHub, import ke Vercel.
3. Environment variables:
   - `DATABASE_URL`
   - `NEXT_PUBLIC_ROBINHOOD_CHAIN_ID`, `NEXT_PUBLIC_ROBINHOOD_RPC_URL`
   - `NEXT_PUBLIC_PREDICTION_CONTRACT_ADDRESS`
   - `NEXT_PUBLIC_TOKEN_CONTRACT_ADDRESS`
   - `ADMIN_WALLET_ADDRESS`
4. Deploy, uji check-in/quest/bet/claim end-to-end dengan jumlah kecil di mainnet sebelum promosi.

## 14. Kriteria Sukses / Definition of Done
- Flow check-in, quest, dan leaderboard poin berjalan tanpa bug.
- Minimal beberapa prediction market selesai siklus penuh (create → bet → resolve → claim) tanpa bug dana macet.
- Admin panel aman, hanya bisa diakses wallet admin.

## 15. Catatan Biaya / Free-Tier untuk Setup Awal
- **RPC Robinhood Chain/testnet**: pakai RPC publik gratis dulu (PublicNode, 1RPC.io, dRPC).
- **Test ETH**: gratis lewat faucet di bagian 12 di atas.
- **Database**: Neon atau Supabase free tier sudah cukup untuk tahap awal (poin & quest cukup ringan datanya).
