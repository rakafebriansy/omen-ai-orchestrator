# Development Planning — Omen

Dokumen ini merinci peta jalan (*roadmap*) pengembangan untuk node **Omen** dalam **MODE 1 (Autonomous Planning)**.

---

## 1. Fase 1: Minimum Viable Product (MVP)

Fase 1 berfokus pada pembangunan fondasi ganda: smart contract pasar prediksi yang teruji aman di testnet dan sistem gamifikasi perolehan poin/misi harian terintegrasi Supabase.

### Strategi Eksekusi: Frontend-First Workflow

Sesuai arahan, alur pengerjaan dipisahkan secara tegas menjadi **Frontend Dulu Secara Penuh (All UI/UX dan Client States)**, baru kemudian melangkah ke pembangunan **Backend Engine (Database dan API)**, **Smart Contract (On-Chain)**, dan diakhiri dengan **Integrasi Web3 Penuh**.

Setiap tiket dirancang memiliki **satu tanggung jawab tunggal (single responsibility)** tanpa menggabungkan dua tugas berbeda dalam satu tiket, agar cakupannya terukur dan mudah dieksekusi.

```
[Tahap 1: Frontend Dulu (22 Tiket)] ──► [Tahap 2: Backend dan DB (12 Tiket)] ──► [Tahap 3: Smart Contract (4 Tiket)] ──► [Tahap 4: Wiring dan E2E (6 Tiket)] ──► [Tahap 5: Live Data & Setup (9 Tiket)]
```

---

### Daftar Backlog Tiket Fase 1

#### 1. Tahap 1: Full Frontend Development (Dikerjakan Pertama)
Fokus pada antarmuka visual, interaktivitas komponen, palet tema OpenZeppelin, dan mock state klien sebelum menyentuh backend.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 1 | **[TICKET-01](../tickets/TICKET-01-setup-nextjs-tailwind-theme.md)** | Setup Next.js dan Tailwind v4 OpenZeppelin Theme | High | `omen/web/globals.css`, `postcss.config.mjs` |
| 2 | **[TICKET-02](../tickets/TICKET-02-setup-vitest-testing-suite.md)** | Setup Testing Suite Vitest | High | `omen/web/vitest.config.ts` |
| 3 | **[TICKET-03](../tickets/TICKET-03-layout-shell-navbar-footer.md)** | Pembuatan Layout Shell Navbar dan Footer | High | `omen/web/app/layout.tsx`, `Navbar.tsx`, `Footer.tsx` |
| 4 | **[TICKET-04](../tickets/TICKET-04-landing-overview-page.md)** | Pembuatan Halaman Landing dan Statistik Platform | High | `omen/web/app/page.tsx`, `HeroSection.tsx` |
| 5 | **[TICKET-05](../tickets/TICKET-05-connect-wallet-button-ui.md)** | Pembuatan Komponen Tombol Connect Wallet | High | `omen/web/components/ConnectWalletButton.tsx` |
| 6 | **[TICKET-06](../tickets/TICKET-06-network-switcher-dialog-ui.md)** | Pembuatan Dialog Network Switcher Phantom EVM | Medium | `omen/web/components/NetworkSwitcherModal.tsx` |
| 7 | **[TICKET-07](../tickets/TICKET-07-daily-checkin-widget-ui.md)** | Pembuatan Widget Daily Check-in Streak | Medium | `omen/web/components/DailyCheckinWidget.tsx` |
| 8 | **[TICKET-08](../tickets/TICKET-08-quest-list-cards-ui.md)** | Pembuatan Komponen Kartu Quest | Medium | `omen/web/components/QuestCard.tsx` |
| 9 | **[TICKET-09](../tickets/TICKET-09-quests-farming-page.md)** | Pembuatan Halaman Quests dan Farming | Medium | `omen/web/app/quests/page.tsx` |
| 10 | **[TICKET-10](../tickets/TICKET-10-points-leaderboard-table-ui.md)** | Pembuatan Tabel Ranking Leaderboard Poin | Medium | `omen/web/components/LeaderboardTable.tsx` |
| 11 | **[TICKET-11](../tickets/TICKET-11-points-leaderboard-page.md)** | Pembuatan Halaman Leaderboard | Medium | `omen/web/app/leaderboard/page.tsx` |
| 12 | **[TICKET-12](../tickets/TICKET-12-market-category-filter-ui.md)** | Pembuatan Komponen Filter Kategori Pasar Prediksi | High | `omen/web/components/MarketCategoryFilter.tsx` |
| 13 | **[TICKET-13](../tickets/TICKET-13-prediction-market-card-ui.md)** | Pembuatan Komponen Kartu Pasar Prediksi | High | `omen/web/components/MarketCard.tsx` |
| 14 | **[TICKET-14](../tickets/TICKET-14-prediction-markets-feed-page.md)** | Pembuatan Halaman Katalog Pasar Prediksi | High | `omen/web/app/predictions/page.tsx` |
| 15 | **[TICKET-15](../tickets/TICKET-15-betting-modal-dialog-ui.md)** | Pembuatan Modal Dialog Pasang Taruhan | High | `omen/web/components/BettingModal.tsx` |
| 16 | **[TICKET-16](../tickets/TICKET-16-user-bets-table-ui.md)** | Pembuatan Tabel Riwayat Taruhan Pengguna | High | `omen/web/components/UserBetsTable.tsx` |
| 17 | **[TICKET-17](../tickets/TICKET-17-payout-claim-button-ui.md)** | Pembuatan Komponen Tombol Klaim Payout | High | `omen/web/components/ClaimPayoutButton.tsx` |
| 18 | **[TICKET-18](../tickets/TICKET-18-my-bets-page.md)** | Pembuatan Halaman My Bets | High | `omen/web/app/my-bets/page.tsx` |
| 19 | **[TICKET-19](../tickets/TICKET-19-admin-market-create-form-ui.md)** | Pembuatan Form Admin Pembuatan Pasar Prediksi | Medium | `omen/web/components/AdminMarketCreateForm.tsx` |
| 20 | **[TICKET-20](../tickets/TICKET-20-admin-quest-management-form-ui.md)** | Pembuatan Form Admin Manajemen Quest | Medium | `omen/web/components/AdminQuestManagementForm.tsx` |
| 21 | **[TICKET-21](../tickets/TICKET-21-admin-market-resolution-ui.md)** | Pembuatan Interface Admin Resolusi Pasar Prediksi | Medium | `omen/web/components/AdminMarketResolutionTable.tsx` |
| 22 | **[TICKET-22](../tickets/TICKET-22-admin-dashboard-page.md)** | Pembuatan Halaman Admin Dashboard | Medium | `omen/web/app/admin/page.tsx` |
| 45 | **[TICKET-45](../tickets/TICKET-45-integrate-omen-brand-logo.md)** | Integrasi Logo Resmi Omen pada Navbar, Footer, dan Shell Branding | Medium | `omen/web/components/Navbar.tsx`, `Footer.tsx` |

#### 2. Tahap 2: Backend Engine dan Basis Data (Off-Chain)
Membangun skema tabel persistensi di Supabase dan Route Handlers API per fungsionalitas tunggal.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 23 | **[TICKET-23](../tickets/TICKET-23-supabase-schema-migration.md)** | Skema Basis Data Supabase Migration | High | `omen/web/db/migrations/01_init_schema.sql` |
| 24 | **[TICKET-24](../tickets/TICKET-24-supabase-database-client-helper.md)** | Pembuatan Supabase Database Client Helper | High | `omen/web/lib/supabase.ts`, `database.ts` |
| 25 | **[TICKET-25](../tickets/TICKET-25-api-wallet-connect-upsert.md)** | Pembuatan API Route Pendaftaran Wallet | High | `omen/web/app/api/wallet/connect/route.ts` |
| 26 | **[TICKET-26](../tickets/TICKET-26-api-daily-checkin-streak.md)** | Pembuatan API Route Daily Check-in Streak | Medium | `omen/web/app/api/checkin/route.ts` |
| 27 | **[TICKET-27](../tickets/TICKET-27-api-quests-list.md)** | Pembuatan API Route Daftar Quest | Medium | `omen/web/app/api/quests/route.ts` |
| 28 | **[TICKET-28](../tickets/TICKET-28-api-quest-completion-verification.md)** | Pembuatan API Route Verifikasi Quest | Medium | `omen/web/app/api/quests/[id]/complete/route.ts` |
| 29 | **[TICKET-29](../tickets/TICKET-29-api-points-leaderboard.md)** | Pembuatan API Route Ranking Poin | Medium | `omen/web/app/api/leaderboard/points/route.ts` |
| 30 | **[TICKET-30](../tickets/TICKET-30-api-markets-get-feed.md)** | Pembuatan API Route Katalog Pasar | High | `omen/web/app/api/markets/route.ts` |
| 31 | **[TICKET-31](../tickets/TICKET-31-api-markets-post-create.md)** | Pembuatan API Route Simpan Pasar Baru | Medium | `omen/web/app/api/markets/route.ts` |
| 32 | **[TICKET-32](../tickets/TICKET-32-api-markets-resolve-status.md)** | Pembuatan API Route Pembaruan Status Pasar | Medium | `omen/web/app/api/markets/[id]/resolve/route.ts` |
| 33 | **[TICKET-33](../tickets/TICKET-33-api-user-bets-get.md)** | Pembuatan API Route Riwayat Taruhan | High | `omen/web/app/api/bets/route.ts` |
| 34 | **[TICKET-34](../tickets/TICKET-34-api-bets-indexer.md)** | Pembuatan API Route Indexer Taruhan | High | `omen/web/app/api/bets/index/route.ts` |

#### 3. Tahap 3: Smart Contract dan Deployment (On-Chain)
Mempersiapkan lingkungan Hardhat, mengimplementasikan kontrak `PredictionMarket.sol`, menjalankan unit testing, dan mendeploy ke testnet.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 35 | **[TICKET-35](../tickets/TICKET-35-hardhat-setup-arbitrum-sepolia.md)** | Inisialisasi Hardhat dan Konfigurasi Arbitrum Sepolia | High | `omen/contracts/hardhat.config.ts`, `package.json` |
| 36 | **[TICKET-36](../tickets/TICKET-36-prediction-market-contract-implementation.md)** | Implementasi Smart Contract PredictionMarket.sol | High | `omen/contracts/contracts/PredictionMarket.sol` |
| 37 | **[TICKET-37](../tickets/TICKET-37-hardhat-contract-unit-testing.md)** | Unit Testing Hardhat PredictionMarket.sol | High | `omen/contracts/test/PredictionMarket.test.ts` |
| 38 | **[TICKET-38](../tickets/TICKET-38-testnet-deployment-abi-export.md)** | Script Deployment Testnet dan Ekspor ABI | High | `omen/contracts/scripts/deploy.ts`, `contracts.ts` |

#### 4. Tahap 4: Full Wiring Web3 dan Validasi End-to-End
Menghubungkan tombol aksi di frontend ke fungsi smart contract testnet dan memvalidasi siklus penuh di browser.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 39 | **[TICKET-39](../tickets/TICKET-39-web3-provider-wagmi-integration.md)** | Integrasi Web3 Provider Wagmi di Layout Web | High | `omen/web/app/providers.tsx`, `wagmi.ts` |
| 40 | **[TICKET-40](../tickets/TICKET-40-web3-betting-transaction-wiring.md)** | Integrasi Transaksi Taruhan pada Betting Modal | High | `omen/web/components/BettingModal.tsx`, `usePlaceBet.ts` |
| 41 | **[TICKET-41](../tickets/TICKET-41-web3-claim-payout-wiring.md)** | Integrasi Transaksi Klaim pada Halaman My Bets | High | `omen/web/components/ClaimPayoutButton.tsx`, `useClaimPayout.ts` |
| 42 | **[TICKET-42](../tickets/TICKET-42-admin-create-market-wiring.md)** | Integrasi Transaksi Admin Pembuatan Pasar | Medium | `omen/web/components/AdminMarketCreateForm.tsx` |
| 43 | **[TICKET-43](../tickets/TICKET-43-admin-resolve-market-wiring.md)** | Integrasi Transaksi Admin Resolusi Pasar | Medium | `omen/web/components/AdminMarketResolutionTable.tsx` |
| 44 | **[TICKET-44](../tickets/TICKET-44-testnet-e2e-browser-validation.md)** | Validasi Siklus Hidup Penuh End-to-End di Browser | High | `omen/web/tests/e2e/workflow.test.ts` |

#### 5. Tahap 5: Full Mock Web3 Engine & Real Supabase Live Data Wiring
Menghubungkan seluruh alur aplikasi frontend dengan basis data Supabase aktif, mengimplementasikan Mock Contract & Web3 Simulator Engine untuk pengujian end-to-end tanpa gas fee/ketergantungan ekstensi browser.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 46 | **[TICKET-46](../tickets/TICKET-46-manual-supabase-provisioning-and-migration.md)** *(DONE)* | Penyediaan Kredensial Supabase & Eksekusi Skema Migrasi Basis Data | High | `omen/web/.env.local`, `01_init_schema.sql` |
| 47 | **[TICKET-47](../tickets/TICKET-47-mock-contract-and-web3-simulator-engine.md)** *(DONE)* | Implementasi Mock Contract Engine & Web3 Simulator Provider | High | `omen/web/lib/mockPredictionMarket.ts`, `contracts.ts` |
| 48 | **[TICKET-48](../tickets/TICKET-48-mock-wallet-connection-and-supabase-sync.md)** *(DONE)* | Integrasi Mock Wallet Connection & Auto-Registration ke Supabase | High | `omen/web/components/ConnectWalletButton.tsx`, `Navbar.tsx` |
| 49 | **[TICKET-49](../tickets/TICKET-49-predictions-feed-api-and-mock-betting-integration.md)** *(DONE)* | Integrasi Real Supabase Feed & Mock Betting Flow pada Halaman Predictions | High | `omen/web/app/predictions/page.tsx`, `BettingModal.tsx` |
| 50 | **[TICKET-50](../tickets/TICKET-50-quests-daily-checkin-api-database-integration.md)** *(DONE)* | Integrasi Real Data & API Mutation pada Halaman Quests & Daily Check-in | High | `omen/web/app/quests/page.tsx`, `DailyCheckinWidget.tsx` |
| 51 | **[TICKET-51](../tickets/TICKET-51-leaderboard-points-api-database-integration.md)** *(DONE)* | Integrasi Real Leaderboard & Ranking User pada Halaman Leaderboard | Medium | `omen/web/app/leaderboard/page.tsx` |
| 52 | **[TICKET-52](../tickets/TICKET-52-my-bets-user-history-api-database-integration.md)** *(DONE)* | Integrasi Real User Betting History pada Halaman My Bets | High | `omen/web/app/my-bets/page.tsx` |
| 53 | **[TICKET-53](../tickets/TICKET-53-admin-quest-api-and-metrics-integration.md)** *(DONE)* | Pembuatan API Route Admin Quests & Integrasi Live Metrics Admin Dashboard | Medium | `omen/web/app/api/admin/quests/route.ts`, `AdminQuestManagementForm.tsx`, `app/admin/page.tsx` |
| 54 | **[TICKET-54](../tickets/TICKET-54-landing-page-live-statistics-integration.md)** *(DONE)* | Integrasi Live Platform Statistics pada Landing Page | Low | `omen/web/components/landing/StatsOverview.tsx`, `TrendingMarketsTeaser.tsx` |

#### 6. Tahap 6: Live Testnet Activation (Pasca-MVP)
Aktivasi smart contract on-chain di jaringan Arbitrum Sepolia dan integrasi live wallet browser.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 55 | **[TICKET-55](../tickets/TICKET-55-manual-arbitrum-sepolia-contract-deployment.md)** *(MANUAL)* | Deployment Smart Contract ke Arbitrum Sepolia Testnet & Verifikasi Arbiscan | High | `omen/contracts/.env`, `deploy.ts`, `contracts.ts` |
| 56 | **[TICKET-56](../tickets/TICKET-56-real-web3-wallet-connection-integration.md)** | Integrasi Real Wagmi Web3 Wallet Connection & Network Switcher | High | `omen/web/components/ConnectWalletButton.tsx`, `NetworkSwitcherModal.tsx` |
| 57 | **[TICKET-57](../tickets/TICKET-57-real-web3-live-onchain-switch.md)** | Real On-Chain Contract Wiring (Switch Mock Engine ke Live Arbitrum Sepolia) | High | `omen/web/.env.local`, `usePlaceBet.ts`, `useClaimPayout.ts` |

---

## 2. Fase 2: Advanced Utilities (Masa Depan)

1. Sistem Referral Multiplier (poin berjenjang untuk pengundang dan yang diundang).
2. Automated Price Feed Oracle (integrasi Pyth / Chainlink untuk pasar berbasis harga crypto otomatis).
3. Leaderboard Prediktor Terbaik (ranking akurasi win-rate terpisah).
4. Token Reward Claim Engine (konversi poin ke token reward on-chain).


