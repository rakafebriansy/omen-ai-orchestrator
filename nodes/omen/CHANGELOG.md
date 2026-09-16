# CHANGELOG — Omen

Changelog berfungsi sebagai catatan riwayat perubahan untuk node **Omen**.

## Kategori Perubahan

*   **Guideline: <judul>**: Perubahan atau penambahan pada dokumen panduan.
*   **PRD**: Perubahan pada Product Requirements Document.
*   **Design System**: Pembaruan atau modifikasi Design System.
*   **System Design**: Perubahan pada arsitektur atau System Design.
*   **Development Planning: <nomor>**: Pembaruan pada perencanaan pengembangan.
*   **Ticket: <nomor>**: Perbaikan atau penambahan fitur yang merujuk pada tiket tertentu.
*   **Prototype: <judul>**: Pembaruan atau pembuatan prototipe desain/aplikasi.
*   **Implementation**: Implementasi coding pada codebase aplikasi.

## Log Perubahan (Omen)

*(⚠️ PERHATIAN AI AGENT: TAMBAHKAN ENTRI LOG BARU ANDA TEPAT DI BAWAH BARIS INI. JANGAN DI PALING BAWAH DOKUMEN!)*

### [2026-09-16 07:30:00] - Implementation: TICKET-04 Dual Theme Dark Emerald dan Light Emerald Landing Page
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "berikut yang saya unggah adalah prompt kedua, dimana untuk membuat light mode dan dark mode, juga memperbaiki tampilan menjadi gradient background. ikutilah prompt tersebut dan sesuaikan dengan konteks app kita"
- **Perubahan:** `[Added]` Mengimplementasikan sistem tema ganda (Dark Emerald Mode dan Light Emerald Mode) pada Landing Page Hero dan ekosistem Web3 Omen. Menghasilkan dua aset 3D render fotorealistik (`public/images/hero-dark-emerald.jpg` dan `public/images/hero-light-emerald.png`), mengimplementasikan `ThemeProvider.tsx`, memperbarui `globals.css` dengan token warna Dark Emerald (`#030906`, `#0A0F0C`, `#34D399`, `#047857`) dan Light Emerald (`#CFF3E2`, `#A9EAC9`, `#0B1F16`, `#10221A`, `#0E7A4E`) beserta layered CSS gradients, merancang `HeroSection.tsx` dengan layout Centered Stack (Dark Mode) dan Left-Aligned Split (Light Mode), memperbarui `Navbar.tsx` dengan theme switcher toggle, serta menyelaraskan seluruh subkomponen (`StatsOverview.tsx`, `FeaturePillars.tsx`, `TrendingMarketsTeaser.tsx`, `QuestsTeaser.tsx`, `AirdropBanner.tsx`, `Footer.tsx`). Menambahkan unit testing di `tests/landing.test.tsx` dan `tests/navbar.test.tsx` (23 tests passing 100% pada Vitest).
- **Path File:** `omen/web/app/page.tsx`, `omen/web/app/layout.tsx`, `omen/web/app/globals.css`, `omen/web/components/ThemeProvider.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/components/landing/HeroSection.tsx`, `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/components/landing/AirdropBanner.tsx`, `omen/web/public/images/hero-dark-emerald.jpg`, `omen/web/public/images/hero-light-emerald.png`, `omen/web/tests/landing.test.tsx`, `omen/web/tests/navbar.test.tsx`, `nodes/omen/tickets/TICKET-04-landing-overview-page.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-16 06:40:00] - Implementation: TICKET-04 Landing Overview Page Dark Premium Hero
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "bacalah prompt di atas sebagai referensi style, buatkan landing page @page.tsx terbaik untuk konteks project web3 ini dengan kata kunci: betting, airdrop, crypto, gamification, quest"
- **Perubahan:** `[Added]` Mengimplementasikan Landing Page utama berestetika Dark Premium Luxury Hero (Wealthfront dan OpenZeppelin Style) di `omen/web` pada rute `app/page.tsx`. Menghasilkan aset 3D render fotorealistik (`public/images/hero-bg.jpg`), membuat komponen `HeroSection.tsx` dengan framed panel `#07090E`, glowing amber seam border, dan tipografi masif `clamp(42px, 7.5vw, 96px)`, `StatsOverview.tsx` dengan 4 metrik on-chain, `FeaturePillars.tsx` pilar ganda platform, `TrendingMarketsTeaser.tsx` dengan live odds Yes/No, `QuestsTeaser.tsx` dengan kalender 7-day streak dan instant tasks, serta `AirdropBanner.tsx` untuk kampanye airdrop Season 1. Menyelaraskan `Navbar.tsx` menjadi floating pill dan `globals.css` dengan latar true black `#000000`. Menambahkan unit testing di `tests/landing.test.tsx` (21 tests passing 100% pada Vitest).
- **Path File:** `omen/web/app/page.tsx`, `omen/web/components/landing/HeroSection.tsx`, `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/components/landing/AirdropBanner.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/app/globals.css`, `omen/web/public/images/hero-bg.jpg`, `omen/web/tests/landing.test.tsx`, `nodes/omen/tickets/TICKET-04-landing-overview-page.md`, `nodes/omen/CHANGELOG.md`


### [2026-09-15 23:10:00] - Implementation: TICKET-03 Layout Shell Navbar dan Footer
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan @TICKET-03-layout-shell-navbar-footer.md"
- **Perubahan:** `[Added]` Mengimplementasikan layout shell aplikasi berestetika OpenZeppelin Institutional Web3 di `omen/web`. Membuat komponen sticky `Navbar.tsx` dengan backdrop blur, logo Omen, badge status Testnet, deteksi rute aktif, slot tombol Connect Wallet, dan responsive hamburger drawer mobile. Membuat komponen `Footer.tsx` 4 kolom responsif (Brand dan indikator status Arbitrum Sepolia berdenyut, Platform, Developers, Community) beserta disclaimer. Mengintegrasikan `layout.tsx` dengan sticky footer layout. Menambahkan unit testing Vitest di `tests/navbar.test.tsx` dan `tests/footer.test.tsx` (15 tests passing, 100% test coverage).
- **Path File:** `omen/web/app/layout.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/tests/navbar.test.tsx`, `omen/web/tests/footer.test.tsx`, `nodes/omen/tickets/TICKET-03-layout-shell-navbar-footer.md`, `nodes/omen/CHANGELOG.md`


### [2026-09-15 22:50:00] - Testing: TICKET-02 Setup Testing Suite Vitest
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan @TICKET-02-setup-vitest-testing-suite.md"
- **Perubahan:** `[Added]` Mengonfigurasi test runner Vitest, `@testing-library/react`, `@testing-library/jest-dom`, `@vitejs/plugin-react`, dan jsdom di `omen/web`. Menambahkan konfigurasi `vitest.config.mts`, `tests/setup.ts`, sampel unit test `tests/sample.test.tsx`, serta script `npm run test`, `test:watch`, dan `test:coverage` di `package.json`.
- **Path File:** `omen/web/package.json`, `omen/web/package-lock.json`, `omen/web/vitest.config.mts`, `omen/web/tests/setup.ts`, `omen/web/tests/sample.test.tsx`, `nodes/omen/tickets/TICKET-02-setup-vitest-testing-suite.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-15 22:10:00] - Implementation: TICKET-01 Setup Next.js dan Tailwind v4 OpenZeppelin Theme
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/rakafebriansy/omen-ai-orchestrator.git`
- **Konteks:** "implementasikan @implementation_plan.md di branch main"
- **Perubahan:** `[Added]` Mengonfigurasi TypeScript (strict mode, `@/*` alias) dan Tailwind CSS v4 CSS-first (`@theme`) dengan palet tema OpenZeppelin Institutional Web3 di `omen/web`. Mengonversi `layout.js` dan `page.js` menjadi `layout.tsx` dan `page.tsx`, menambahkan `postcss.config.mjs`, serta membersihkan file lama `page.module.css` dan `jsconfig.json`.
- **Path File:** `omen/web/package.json`, `omen/web/tsconfig.json`, `omen/web/postcss.config.mjs`, `omen/web/app/globals.css`, `omen/web/app/layout.tsx`, `omen/web/app/page.tsx`, `nodes/omen/tickets/TICKET-01-setup-nextjs-tailwind-theme.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-15 19:51:00] - Design System: OpenZeppelin Theme Migration
> **Trigger:** Prompt Driven | **Branch:** `main` | **Repo:** `https://github.com/rakafebriansy/omen-ai-orchestrator.git`
- **Konteks:** "ganti tema nya dari cyberpunk ke seperti web ini: https://www.openzeppelin.com/solidity-contracts?ref=landingfolio"
- **Perubahan:** `[Changed]` Memperbarui seluruh pedoman visual dan token desain dari tema Cyberpunk Glassmorphism menjadi **OpenZeppelin Institutional Web3 / Developer-First Aesthetic** (Clean White `#FFFFFF` surface, Slate `#0F172A`, Royal Cobalt `#4E5EE4`, Emerald `#10B981`, Rose `#F43F5E`, crisp 1px borders, typography Inter + JetBrains Mono). Menyelaraskan dokumen `global-docs/design-system.md`, `global-docs/ui-example.md`, `global-docs/prd.md`, `nodes/omen/guidelines/project-context.md`, `nodes/omen/docs/system-design.md`, dan tiket terkait (`TICKET-01`, `TICKET-08`).
- **Path File:** `global-docs/design-system.md`, `global-docs/ui-example.md`, `global-docs/prd.md`, `nodes/omen/guidelines/project-context.md`, `nodes/omen/docs/system-design.md`, `nodes/omen/tickets/TICKET-01-web-typescript-tailwind-setup.md`, `nodes/omen/tickets/TICKET-08-points-leaderboard-ui.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-15 15:31:00] - Initialization: Single-Project Environment Node Setup
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/rakafebriansy/omen-ai-orchestrator.git`
- **Konteks:** "Saya ingin menginisialisasi Single-Project Environment menggunakan kerangka kerja AI Orchestrator ini. Nama Sistem: Omen. Mode 1 (Autonomous Planning)."
- **Perubahan:** `[Added]` Menginisialisasi node utama `nodes/omen/` untuk sistem Points/Quest Farming + Prediction Market Dashboard Omen. Membuat dokumen fondasi terisolasi mencakup `nodes/omen/main.md` dengan status aktif MODE 1, `nodes/omen/guidelines/project-context.md` dari hasil pemindaian struktur monorepo (`omen/contracts` & `omen/web`), `nodes/omen/docs/system-design.md` beserta 4 diagram arsitektur PlantUML (`erd.puml`, `flowchart.puml`, `state-diagram.puml`, `sequence-diagram.puml`), `nodes/omen/docs/development-planning.md` dengan 12 tiket backlog Fase 1 (`TICKET-01` s/d `TICKET-12`), dan menyelaraskan `global-docs/prd.md` serta `global-docs/design-system.md` dan diagram global (`user-journey.puml`, `use-case.puml`).
- **Path File:** `nodes/omen/main.md`, `nodes/omen/CHANGELOG.md`, `nodes/omen/guidelines/project-context.md`, `nodes/omen/docs/system-design.md`, `nodes/omen/docs/development-planning.md`, `nodes/omen/tickets/TICKET-01-web-typescript-tailwind-setup.md`, `nodes/omen/tickets/TICKET-02-hardhat-smart-contract-setup.md`, `nodes/omen/tickets/TICKET-03-supabase-schema-migration.md`, `nodes/omen/tickets/TICKET-04-prediction-market-contract.md`, `nodes/omen/tickets/TICKET-05-contract-unit-testing.md`, `nodes/omen/tickets/TICKET-06-wallet-connect-wagmi.md`, `nodes/omen/tickets/TICKET-07-daily-checkin-quest-api.md`, `nodes/omen/tickets/TICKET-08-points-leaderboard-ui.md`, `nodes/omen/tickets/TICKET-09-prediction-market-list-ui.md`, `nodes/omen/tickets/TICKET-10-betting-claim-flow.md`, `nodes/omen/tickets/TICKET-11-admin-market-resolver.md`, `nodes/omen/tickets/TICKET-12-testnet-e2e-deployment.md`, `nodes/omen/docs/diagrams/erd.puml`, `nodes/omen/docs/diagrams/flowchart.puml`, `nodes/omen/docs/diagrams/state-diagram.puml`, `nodes/omen/docs/diagrams/sequence-diagram.puml`, `global-docs/prd.md`, `global-docs/design-system.md`, `global-docs/diagrams/user-journey.puml`, `global-docs/diagrams/use-case.puml`
