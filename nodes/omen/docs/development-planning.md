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

#### 5.1 Tahap 5.1: Pembersihan Data Statis & Full Dynamic API Integration
Menghapus seluruh fallback array statis (hardcoded dummy data) di semua halaman dan komponen, serta mengintegrasikan murni secara dinamis dengan API backend dan Supabase.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 58 | **[TICKET-58](../tickets/TICKET-58-quests-dynamic-data-and-user-profile-integration.md)** *(DONE)* | Integrasi Dynamic Data Supabase & User Profile pada Halaman Quests | High | `omen/web/app/quests/page.tsx`, `DailyCheckinWidget.tsx` |
| 59 | **[TICKET-59](../tickets/TICKET-59-leaderboard-dynamic-data-and-podium-calculation.md)** *(DONE)* | Integrasi Dynamic Leaderboard & Kalkulasi Podium Real-time dari Supabase | High | `omen/web/app/leaderboard/page.tsx`, `LeaderboardTable.tsx` |
| 60 | **[TICKET-60](../tickets/TICKET-60-my-bets-dynamic-portfolio-and-metric-calculation.md)** *(DONE)* | Integrasi Dynamic Portfolio My Bets & Kalkulasi Metrik Portofolio Real-time | High | `omen/web/app/my-bets/page.tsx`, `UserBetsTable.tsx` |
| 61 | **[TICKET-61](../tickets/TICKET-61-predictions-feed-pure-dynamic-loading-and-category-sync.md)** *(DONE)* | Integrasi Pure Dynamic Feed Pasar Prediksi & Sinkronisasi Filter Kategori | High | `omen/web/app/predictions/page.tsx` |
| 62 | **[TICKET-62](../tickets/TICKET-62-landing-page-teasers-api-sync.md)** *(DONE)* | Integrasi Live API Data pada Trending Markets Teaser dan Quests Teaser Landing Page | Medium | `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `QuestsTeaser.tsx` |
| 63 | **[TICKET-63](../tickets/TICKET-63-admin-resolution-and-quest-forms-api-sync.md)** *(DONE)* | Integrasi Live API Data pada Admin Market Resolution Table & Quest Management Form | Medium | `omen/web/components/AdminMarketResolutionTable.tsx`, `AdminQuestManagementForm.tsx`, `app/admin/page.tsx` |

#### 6. Tahap 6: Live Testnet Activation (Telah Digantikan oleh Arsitektur V1 Dual-Testnet)
*Catatan: Rencana legacy deployment Arbitrum Sepolia (TICKET-55) telah dihapus dan digantikan oleh arsitektur Dual-Testnet Foundry V1 (Ethereum Sepolia di TICKET-101 & Robinhood Chain Testnet di TICKET-98).*

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 56 | **[TICKET-56](../tickets/TICKET-56-real-web3-wallet-connection-integration.md)** *(DONE via TICKET-64)* | Integrasi Real Wagmi Web3 Wallet Connection & Network Switcher | High | `omen/web/components/ConnectWalletButton.tsx`, `NetworkSwitcherModal.tsx` |
| 57 | **[TICKET-57](../tickets/TICKET-57-real-web3-live-onchain-switch.md)** *(DONE via TICKET-93..101)* | Real On-Chain Contract Wiring (Dual-Testnet Sepolia & Robinhood) | High | `omen/web/.env.local`, `usePlaceBet.ts`, `useClaimPayout.ts` |

---

## 2. Fase V1: Social Belief Market Protocol Transformation

Fase V1 mentransformasikan platform OMEN menjadi **Social Belief Market Protocol** terdesentralisasi multi-chain (Ethereum Sepolia + Robinhood Chain Testnet 46630), beralih dari prediksi biner biasa ke pasar keyakinan sosial (AGREE/DISAGREE), orakel deterministik Chainlink, dan konfirmasi kreator EIP-712.

> ⚡ **Multi-Agent Parallel Execution Plan:**
> Untuk pemetaan alur eksekusi paralel 4 AI Agent (Smart Contract, Backend, Frontend UI, dan Web3 Integrator) beserta matriks dependensi antar-tiket lengkap (DAG), lihat dokumen:
> 👉 **[v1-parallel-execution-plan.md](./v1-parallel-execution-plan.md)**

### Strategi Eksekusi V1

```
[P00: Foundation Refactor (3 Tiket)]
  │
  ├──► [P01: Smart Contracts Foundry (5 Tiket)]
  │
  ├──► [P02: Frontend Core Beliefs UI (11 Tiket)]
  │       │
  │       └──► [P03: Backend API V1 Supabase (10 Tiket)]
  │
  ├──► [P03.5: Web3 Wagmi Hooks (2 Tiket)]
  │
  ├──► [P04: Oracle Chainlink & Resolution Engine (2 Tiket)]
  │
  ├──► [P05: Creator Confirmation EIP-712 (1 Tiket)]
  │
  └──► [P06: Robinhood Chain & Dual-Testnet E2E (3 Tiket)]
```

> 🎨 **Prinsip Desain Visual V1:**
> Seluruh implementasi tiket UI **WAJIB MEMPERTAHANKAN** tema OpenZeppelin dark mode, palet warna, tipografi, efek glassmorphism, dan komponen UI existing tanpa melakukan rewrite visual dari nol.

---

### Daftar Backlog Tiket V1

#### 1. Phase P00 — Foundation Refactor (Prerequisite)
Menyesuaikan konfigurasi provider, skema basis data 11 tabel, dan kerangka navigasi layout shell.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 64 | **[TICKET-64](../tickets/TICKET-64-refactor-wagmi-config-multi-chain.md)** | Refactor Wagmi Config & Web3 Providers untuk Ethereum Sepolia dan Robinhood Chain Testnet | High | `omen/web/lib/wagmi.ts`, `providers.tsx`, `NetworkSwitcherModal.tsx` |
| 65 | **[TICKET-65](../tickets/TICKET-65-manual-database-schema-v1-beliefs-migration.md)** *(MANUAL)* | (MANUAL) Migrasi Skema Basis Data Supabase V1 (11 Tabel Arsitektur Social Beliefs) | High | `omen/web/db/migrations/02_v1_belief_schema.sql`, `types/database.ts` |
| 66 | **[TICKET-66](../tickets/TICKET-66-refactor-navbar-layout-shell-v1.md)** | Refactor Navbar, Footer & Layout Shell Navigasi V1 | High | `omen/web/components/Navbar.tsx`, `Footer.tsx`, `app/layout.tsx` |

#### 2. Phase P01 — Smart Contract Core (Foundry)
Membangun dan menguji `OmenFactory.sol` dan `OmenMarket.sol` menggunakan Foundry toolkit.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 67 | **[TICKET-67](../tickets/TICKET-67-foundry-initialization-and-multichain-config.md)** | Inisialisasi Lingkungan Foundry & Konfigurasi Multi-Chain | High | `omen/contracts/foundry.toml`, `remappings.txt`, `README.md` |
| 68 | **[TICKET-68](../tickets/TICKET-68-omen-factory-contract-implementation.md)** | Implementasi Smart Contract OmenFactory.sol | High | `omen/contracts/src/OmenFactory.sol`, `IOmenFactory.sol` |
| 69 | **[TICKET-69](../tickets/TICKET-69-omen-market-contract-implementation.md)** | Implementasi Smart Contract OmenMarket.sol | High | `omen/contracts/src/OmenMarket.sol`, `IOmenMarket.sol` |
| 70 | **[TICKET-70](../tickets/TICKET-70-foundry-unit-testing-suite.md)** | Foundry Unit & Invariant Testing Suite untuk OmenFactory dan OmenMarket | High | `omen/contracts/test/OmenFactory.t.sol`, `OmenMarket.t.sol` |
| 71 | **[TICKET-71](../tickets/TICKET-71-mock-smart-contract-abi-export.md)** | Setup Mock Smart Contract Environment, Ekspor Artefak ABI ke Web & Konfigurasi Contracts Helper | High | `omen/web/contracts/`, `web/lib/contracts.ts`, `tests/contracts-abi.test.ts` |

#### 3. Phase P02 — Frontend Core (Belief-Centric UI)
Membangun antarmuka pasar keyakinan sosial (Landing, Markets Feed, Market Detail, Position Panel, Beliefs, Creators, Activity, Submit Wizard).

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 72 | **[TICKET-72](../tickets/TICKET-72-redesign-landing-page-social-belief-hero.md)** | Redesign Landing Page dengan Hero Social Belief & Live Market Feeds | High | `omen/web/app/page.tsx`, `HeroSection.tsx`, `StatsOverview.tsx` |
| 73 | **[TICKET-73](../tickets/TICKET-73-belief-market-card-component.md)** | Pembuatan Komponen BeliefMarketCard (WHO, WHAT, WHEN, CONSENSUS, MONEY) | High | `omen/web/components/BeliefMarketCard.tsx`, `belief-market-card.test.tsx` |
| 74 | **[TICKET-74](../tickets/TICKET-74-discovery-feed-markets-page.md)** | Pembuatan Halaman Discovery Feed Pasar Keyakinan (/markets) & Tab Filter | High | `omen/web/app/markets/page.tsx`, `DiscoveryFilter.tsx` |
| 75 | **[TICKET-75](../tickets/TICKET-75-market-detail-multi-panel-page.md)** | Pembuatan Halaman Market Detail Multi-Panel (/market/[id]) | High | `omen/web/app/market/[id]/page.tsx`, `MarketDetailPanels.tsx` |
| 76 | **[TICKET-76](../tickets/TICKET-76-position-panel-component.md)** | Pembuatan Komponen PositionPanel (AGREE / DISAGREE Inline Flow) | High | `omen/web/components/PositionPanel.tsx`, `position-panel.test.tsx` |
| 77 | **[TICKET-77](../tickets/TICKET-77-beliefs-feed-page.md)** | Pembuatan Halaman Katalog Beliefs (/beliefs) | Medium | `omen/web/app/beliefs/page.tsx`, `beliefs-page.test.tsx` |
| 78 | **[TICKET-78](../tickets/TICKET-78-belief-card-component.md)** | Pembuatan Komponen BeliefCard (Compact Belief & Status Badge) | Medium | `omen/web/components/BeliefCard.tsx`, `belief-card.test.tsx` |
| 79 | **[TICKET-79](../tickets/TICKET-79-creator-profile-page.md)** | Pembuatan Halaman Profil Kreator (/creator/[address]) | Medium | `omen/web/app/creator/[address]/page.tsx`, `CreatorProfileHeader.tsx` |
| 80 | **[TICKET-80](../tickets/TICKET-80-creators-directory-page.md)** | Pembuatan Halaman Direktori & Ranking Kreator (/creators) | Medium | `omen/web/app/creators/page.tsx`, `CreatorCard.tsx` |
| 81 | **[TICKET-81](../tickets/TICKET-81-activity-feed-page.md)** | Pembuatan Halaman Feed Aktivitas Publik On-Chain (/activity) | Medium | `omen/web/app/activity/page.tsx`, `ActivityFeed.tsx` |
| 82 | **[TICKET-82](../tickets/TICKET-82-submit-belief-page-and-form.md)** | Pembuatan Halaman & Formulir Submit Belief 3-Langkah (/create) | High | `omen/web/app/create/page.tsx`, `BeliefSubmitForm.tsx` |

#### 4. Phase P03 — Backend API V1 (Supabase Route Handlers)
Membangun endpoint API serverless V1 untuk belief extraction, submit, markets feed, positions indexer, creator confirmation, ranking, dan resolution.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 83 | **[TICKET-83](../tickets/TICKET-83-api-beliefs-get-list-and-detail.md)** | Pembuatan API Route Beliefs (GET /api/beliefs & GET /api/beliefs/[id]) | High | `omen/web/app/api/beliefs/route.ts`, `api/beliefs/[id]/route.ts` |
| 84 | **[TICKET-84](../tickets/TICKET-84-api-beliefs-ai-extract.md)** | Pembuatan API Route Ekstraksi AI Terstruktur (POST /api/beliefs/extract) | High | `omen/web/app/api/beliefs/extract/route.ts`, `openrouter.ts` |
| 85 | **[TICKET-85](../tickets/TICKET-85-api-beliefs-submit-and-market-creation.md)** | Pembuatan API Route Submit Belief & Trigger On-Chain Market (POST /api/beliefs/submit) | High | `omen/web/app/api/beliefs/submit/route.ts`, `factory-client.ts` |
| 86 | **[TICKET-86](../tickets/TICKET-86-api-markets-v1-get-feed-and-detail.md)** | Refactor API Route Markets V1 (GET /api/markets & GET /api/markets/[id]) | High | `omen/web/app/api/markets/route.ts`, `api/markets/[id]/route.ts` |
| 87 | **[TICKET-87](../tickets/TICKET-87-api-markets-positions-indexer-and-history.md)** | Pembuatan API Route Positions Indexer & History (POST /api/markets/[id]/position & GET /api/positions) | High | `omen/web/app/api/markets/[id]/position/route.ts`, `api/positions/route.ts` |
| 88 | **[TICKET-88](../tickets/TICKET-88-api-creator-confirmation-eip712.md)** | Pembuatan API Route Konfirmasi Kreator EIP-712 (POST /api/beliefs/[id]/confirm) | High | `omen/web/app/api/beliefs/[id]/confirm/route.ts`, `confirmation.ts` |
| 89 | **[TICKET-89](../tickets/TICKET-89-api-creator-profiles-and-directory.md)** | Pembuatan API Route Profil & Direktori Kreator (GET /api/creators & GET /api/creators/[address]) | Medium | `omen/web/app/api/creators/route.ts`, `api/creators/[address]/route.ts` |
| 90 | **[TICKET-90](../tickets/TICKET-90-api-activity-feed-public.md)** | Pembuatan API Route Feed Aktivitas Publik On-Chain (GET /api/activity) | Medium | `omen/web/app/api/activity/route.ts`, `api-activity.test.ts` |
| 91 | **[TICKET-91](../tickets/TICKET-91-api-oracle-price-snapshots.md)** | Pembuatan API Route Snapshot Harga Oracle Chainlink (POST /api/oracle/snapshot) | Medium | `omen/web/app/api/oracle/snapshot/route.ts`, `chainlink.ts` |
| 92 | **[TICKET-92](../tickets/TICKET-92-api-market-resolution-v1.md)** | Refactor API Route Resolusi Pasar V1 (POST /api/markets/[id]/resolve) | High | `omen/web/app/api/markets/[id]/resolve/route.ts`, `resolution-helper.ts` |

#### 5. Phase P03.5 — Web3 Hooks V1
Menyusun custom hooks Wagmi & Viem untuk wiring frontend dengan smart contract `OmenMarket` dan `OmenFactory`.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 93 | **[TICKET-93](../tickets/TICKET-93-web3-hooks-position-claim-market.md)** | Pembuatan Web3 Wagmi Hooks (usePosition, useClaim, useMarket) | High | `omen/web/hooks/usePosition.ts`, `useClaim.ts`, `useMarket.ts` |
| 94 | **[TICKET-94](../tickets/TICKET-94-web3-hook-admin-create-market.md)** | Pembuatan Web3 Wagmi Hook (useCreateMarket untuk OmenFactory) | Medium | `omen/web/hooks/useCreateMarket.ts`, `use-create-market.test.ts` |

#### 6. Phase P04 — Oracle Integration (Chainlink)
Integrasi Chainlink Data Feeds dan engine penyelesaian pasar otomatis berbasis data harga on-chain.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 95 | **[TICKET-95](../tickets/TICKET-95-chainlink-oracle-price-feed-reader.md)** | Integrasi Chainlink Oracle Price Feed Reader (ETH/USD, BTC/USD, SOL/USD) | High | `omen/contracts/src/interfaces/IChainlinkFeed.sol`, `web/lib/oracle/chainlink.ts` |
| 96 | **[TICKET-96](../tickets/TICKET-96-market-resolution-engine-oracle.md)** | Implementasi Market Resolution Engine Berbasis Data Oracle Otomatis | High | `omen/web/lib/market/resolution-engine.ts`, `resolution-engine.test.ts` |

#### 7. Phase P05 — Creator Confirmation (EIP-712)
Alur konfirmasi keyakinan resmi oleh kreator via tanda tangan kriptografis gasless.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 97 | **[TICKET-97](../tickets/TICKET-97-creator-confirmation-flow-ui-and-hook.md)** | Pembuatan Komponen & Hook Konfirmasi Kreator EIP-712 (CreatorConfirmation UI) | Medium | `omen/web/components/CreatorConfirmation.tsx`, `hooks/useCreatorConfirm.ts` |

#### 8. Phase P06 — Robinhood Chain & Multi-Chain E2E Validation
Deployment smart contract ke Robinhood Chain Testnet (46630), pengujian E2E siklus penuh, dan checklist peluncuran.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 98 | **[TICKET-98](../tickets/TICKET-98-mock-contracts-robinhood-chain-testnet.md)** *(DONE)* | Konfigurasi Mock Smart Contract & Simulasi Dual-Chain Robinhood Testnet (Chain ID 46630) | High | `omen/contracts/script/DeployRobinhood.s.sol`, `web/lib/mockContracts.ts` |
| 99 | **[TICKET-99](../tickets/TICKET-99-dual-testnet-e2e-validation.md)** *(DONE)* | Validasi Siklus Hidup Penuh End-to-End pada Dual Testnet (Sepolia & Robinhood Chain) | High | `omen/web/tests/e2e/belief-market-cycle.test.tsx`, `dual-chain-workflow.test.ts` |
| 100 | **[TICKET-100](../tickets/TICKET-100-dummy-environment-variables-and-trust-checklist.md)** *(DONE)* | Konfigurasi Environment Template (Dummy) & Verifikasi Trust Checklist V1 | High | `omen/web/.env.example`, `omen/web/README.md` |
| 101 | **[TICKET-101](../tickets/TICKET-101-manual-foundry-deployment-sepolia.md)** *(DONE)* | Deployment Smart Contract ke Ethereum Sepolia Testnet & Verifikasi Etherscan | High | `omen/contracts/script/DeploySepolia.s.sol`, `omen/web/.env.local` |
| 102 | **[TICKET-102](../tickets/TICKET-102-manual-deploy-contracts-robinhood-chain-testnet.md)** *(DONE)* | Deployment Smart Contract ke Robinhood Chain Testnet (Chain ID 46630) | High | `omen/contracts/script/DeployRobinhood.s.sol`, `omen/web/.env.local` |
| 103 | **[TICKET-103](../tickets/TICKET-103-manual-production-credentials-and-environment-setup.md)** *(DONE)* | Penyediaan Kredensial Nyata & Konfigurasi Environment Production (.env.local) | High | `omen/web/.env.local`, `omen/contracts/.env` |

#### 9. Phase P07 — Production Readiness, Strict Contracts & UI Redesign
Penyempurnaan arsitektur produksi, penghapusan data tiruan (*zero dummy*), migrasi OpenRouter AI, pengetatan kontrak API/BFF, dan restrukturisasi antarmuka pengguna.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 104 | **[TICKET-104](../tickets/TICKET-104-admin-quest-crud-persistence-fix.md)** *(DONE)* | Perbaikan Persistensi CRUD Quest Admin Supabase | High | `omen/web/app/api/admin/quests/route.ts` |
| 105 | **[TICKET-105](../tickets/TICKET-105-admin-market-create-auth-header-fix.md)** *(DONE)* | Standardisasi Header Autentikasi Admin Pembuatan Pasar | High | `omen/web/hooks/useAdminCreateMarket.ts` |
| 106 | **[TICKET-106](../tickets/TICKET-106-admin-market-resolve-auth-header-fix.md)** *(DONE)* | Standardisasi Header Autentikasi Admin Resolusi Pasar | High | `omen/web/hooks/useAdminResolveMarket.ts` |
| 107 | **[TICKET-107](../tickets/TICKET-107-bff-payload-harmonization-bets-positions.md)** *(DONE)* | Harmonisasi Payload BFF untuk Taruhan & Posisi Portofolio | High | `omen/web/app/api/bets/route.ts`, `api/positions/route.ts` |
| 108 | **[TICKET-108](../tickets/TICKET-108-bff-payload-harmonization-beliefs-creator-confirm.md)** *(DONE)* | Harmonisasi Payload BFF untuk Beliefs & Konfirmasi Kreator | High | `omen/web/app/api/beliefs/route.ts`, `confirmation.ts` |
| 109 | **[TICKET-109](../tickets/TICKET-109-eliminate-api-fallbacks-enforce-strict-contracts.md)** *(DONE)* | Eliminasi Fallback Dummy API & Penegakan Strict Schema | High | `omen/web/app/api/markets/route.ts`, `api/activity/route.ts` |
| 110 | **[TICKET-110](../tickets/TICKET-110-frontend-animation-system-implementation.md)** *(DONE)* | Implementasi Sistem Animasi & Transisi Visual Frontend | Medium | `omen/web/globals.css`, `tailwind.config.ts` |
| 111 | **[TICKET-111](../tickets/TICKET-111-live-ai-review-integration-and-free-api-key-setup.md)** *(DONE)* | Integrasi Live AI Review & Konfigurasi Provider OpenRouter | High | `omen/web/lib/ai/openrouter.ts` |
| 112 | **[TICKET-112](../tickets/TICKET-112-redesign-admin-dashboard-protocol-governance-v1.md)** *(DONE)* | Redesain Antarmuka Admin Dashboard & Tata Kelola Protokol V1 | High | `omen/web/app/admin/page.tsx`, `AdminDashboardProps` |
| 113 | **[TICKET-113](../tickets/TICKET-113-creators-directory-supabase-database-integration-fix.md)** *(DONE)* | Integrasi Live Supabase Direktori Kreator & Penanganan Profil | High | `omen/web/app/creators/page.tsx`, `creator.ts` |
| 114 | **[TICKET-114](../tickets/TICKET-114-ai-provider-api-key-cleanup-and-openrouter-migration.md)** *(DONE)* | Pembersihan Kunci AI Provider & Migrasi Terpusat OpenRouter | Medium | `omen/web/.env.local`, `openrouter.ts` |
| 115 | **[TICKET-115](../tickets/TICKET-115-strict-api-contracts-type-migration-and-zero-fallback-enforcement.md)** *(DONE)* | Migrasi Sentralisasi TypeScript Types & Eliminasi Fallback | High | `omen/web/types/*`, `web/lib/*` |
| 116 | **[TICKET-116](../tickets/TICKET-116-fix-market-consensus-and-pool-metrics-zero-state.md)** *(DONE)* | Perbaikan Kalkulasi Konsensus & Metrik Pool State Nol | High | `omen/web/lib/market/consensus.ts` |
| 117 | **[TICKET-117](../tickets/TICKET-117-trending-belief-markets-empty-state-notification.md)** *(DONE)* | Empty State & Notifikasi Trending Belief Markets | Medium | `omen/web/components/landing/TrendingMarketsTeaser.tsx` |
| 118 | **[TICKET-118](../tickets/TICKET-118-live-oracle-feeds-integration-and-light-mode-modal-fix.md)** *(DONE)* | Integrasi Live Oracle Feeds & Perbaikan Kontras Light Mode | High | `omen/web/lib/oracle/chainlink.ts` |
| 119 | **[TICKET-119](../tickets/TICKET-119-optimize-market-detail-light-mode-and-creator-confirmation.md)** *(DONE)* | Optimasi Kontras Market Detail & Banner Konfirmasi Kreator | Medium | `omen/web/components/MarketDetailPanels.tsx` |
| 120 | **[TICKET-120](../tickets/TICKET-120-fix-creator-confirmation-wallet-visibility-and-layout.md)** *(DONE)* | Perbaikan Visibilitas Wallet & Tata Letak Creator Confirmation | Medium | `omen/web/components/CreatorConfirmation.tsx` |
| 121 | **[TICKET-121](../tickets/TICKET-121-update-omen-logo-and-category-tabs-icons.md)** *(DONE)* | Pembaruan Logo Resmi Omen & Ikon Kategori Tabs | Medium | `omen/web/components/Navbar.tsx`, `Footer.tsx` |
| 122 | **[TICKET-122](../tickets/TICKET-122-landing-page-motion-marquee-faq-and-metrics-redesign.md)** *(DONE)* | Redesain Motion Marquee, FAQ Interaktif & Metrik Landing Page | High | `omen/web/app/page.tsx`, `HeroSection.tsx` |

#### 10. Phase P08 — Audit V1 Remediation, Gas Estimation & Error Sanitization
Remediasi komprehensif audit smart contract/backend, estimasi gas on-chain dinamis, sanitasi pesan error UI terpusat, dan integrasi pendaftaran kreator otomatis.

| No | Tiket ID | Judul Tugas Tunggal | Prioritas | Lingkup File |
|:---:|---|---|:---:|---|
| 123 | **[TICKET-123](../tickets/TICKET-123-dynamic-gas-estimation-and-factory-client-optimization.md)** *(DONE)* | Dynamic Gas Estimation & Optimasi OmenFactory Client | High | `omen/web/lib/market/factory-client.ts` |
| 124 | **[TICKET-124](../tickets/TICKET-124-centralized-error-sanitization-and-ui-leak-prevention.md)** *(DONE)* | Sanitasi Error Terpusat & Pencegahan Kebocoran Raw Error Stack di UI | High | `omen/web/lib/format-error.ts`, `BeliefSubmitForm.tsx` |
| 125 | **[TICKET-125](../tickets/TICKET-125-creator-profile-auto-registration-and-x-redirect.md)** *(DONE)* | Registrasi Otomatis Profil Kreator, Backfill DB, dan Integrasi X Redirect | High | `omen/web/app/api/beliefs/submit/route.ts`, `creators/page.tsx` |
| 126 | **[TICKET-126](../tickets/TICKET-126-canonical-database-seed-and-schema-alignment.md)** *(DONE)* | Penyelarasan Skema Kanonikal Database Seed & Data Inisialisasi | Medium | `omen/web/db/seed.sql` |

---

## 3. Fase Masa Depan (Post-V1)

1. Sistem Referral Multiplier & Social Sharing Rewards.
2. Cross-chain Bridge & Liquidity Aggregation.
3. Creator DAO Tokenization & Revenue Share Engine.
4. Autonomous Social Bot Scrapers & Live Stream Integrations.




