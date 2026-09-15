# Project Context & Codebase Scan — Omen

Dokumen ini memuat hasil pemindaian sistem, struktur monorepo, pola arsitektur, pustaka inti, dan pedoman teknis khusus untuk node **Omen**.

---

## 1. Metadata Proyek & Lokasi
* **Nama Node:** `omen`
* **Path Codebase:** `/Users/raka/Developer/repositories/projects/wealthy-people-org/omen-dir/omen`
* **Hosting Frontend:** Vercel
* **Jaringan Blockchain (Testnet):** Arbitrum Sepolia / Robinhood Chain Testnet (EVM)

---

## 2. Struktur Monorepo Codebase

Codebase `omen` diorganisasikan ke dalam dua domain terisolasi:

```
omen/
├── contracts/               # Lingkungan Hardhat & Smart Contracts Solidity
│   ├── contracts/           # Source code contract (PredictionMarket.sol)
│   ├── test/                # Hardhat unit tests (*.test.ts / *.js)
│   ├── scripts/             # Script deployment & verify testnet
│   └── hardhat.config.ts    # Konfigurasi network, RPC, & compiler Solidity
│
└── web/                     # Aplikasi Frontend & Server API (Next.js App Router)
    ├── app/
    │   ├── api/
    │   │   ├── wallet/      # /api/wallet/connect (Upsert user wallet)
    │   │   ├── checkin/     # /api/checkin (Daily streak check-in)
    │   │   ├── quests/      # /api/quests & /api/quests/:id/complete
    │   │   ├── leaderboard/ # /api/leaderboard/points
    │   │   ├── markets/     # /api/markets (GET list, POST create/resolve)
    │   │   └── bets/        # /api/bets (History & indexer endpoint)
    │   ├── admin/           # Halaman Admin Panel terproteksi
    │   ├── leaderboard/     # Halaman Points Leaderboard
    │   ├── predictions/     # Halaman Prediction Market Feed & Detail
    │   ├── quests/          # Halaman Quests & Farming
    │   ├── globals.css      # Tailwind directives & theme configuration
    │   ├── layout.tsx       # Root layout + Wagmi/RainbowKit/Web3 providers
    │   └── page.tsx         # Landing page / Overview
    ├── components/          # Reusable UI components (MarketCard, StreakWidget, BettingModal, etc)
    ├── lib/
    │   ├── supabase.ts      # Supabase client (Database & Auth)
    │   ├── contracts.ts     # ABI, Contract Addresses, & viem/wagmi client configs
    │   └── utils.ts         # Formatting, odds calculator, cn() helper
    ├── public/              # Static brand assets
    └── tailwind.config.ts   # Custom theme tokens & glassmorphic classes
```

---

## 3. Tech Stack & Dependensi Inti

### 3.1 Frontend & API (`web/`)
* **Framework:** Next.js 14+ / 16+ (App Router) dengan TypeScript.
* **Styling:** Tailwind CSS (OpenZeppelin Institutional Web3 / Clean White & Slate theme) + `clsx` / `tailwind-merge`.
* **Web3 & Wallet:** `wagmi`, `viem`, `@tanstack/react-query` (Phantom Wallet EVM Mode).
* **Database Client:** `@supabase/supabase-js` (PostgreSQL Serverless).
* **Testing & Linting:** `vitest` + `@testing-library/react`, `eslint` + `typescript-eslint`.

### 3.2 Smart Contract (`contracts/`)
* **Framework:** Hardhat (`hardhat`, `@nomicfoundation/hardhat-toolbox`, `ethers` / `viem`).
* **Solidity Version:** `^0.8.20`.
* **Testing:** Hardhat Chai/Mocha tests untuk 100% code coverage sebelum migrasi testnet.

---

## 4. Pola Arsitektur Finansial & Keamanan (*Security Ground Truth*)

1. **Non-Custodial Architecture:**
   Semua transaksi taruhan (`placeBet`) dan penarikan kemenangan (`claimPayout`) dieksekusi langsung secara on-chain dari dompet pengguna ke smart contract. Backend web tidak pernah menyimpan *private key* atau menampung dana Native ETH pengguna.
2. **Poin Off-Chain (MVP):**
   Pencatatan poin, riwayat check-in, dan validasi quest disimpan secara efisien di Supabase (tanpa biaya gas blockchain).
3. **Proteksi Akses Admin Panel:**
   Halaman `/admin` dan endpoint admin `/api/markets/resolve` memverifikasi alamat dompet pemanggil terhadap environment variable `ADMIN_WALLET_ADDRESS`.
4. **Kebijakan Testnet-First:**
   Semua kontrak pintar `PredictionMarket.sol` **WAJIB** diuji tuntas di Arbitrum Sepolia sebelum berpindah ke mainnet.
