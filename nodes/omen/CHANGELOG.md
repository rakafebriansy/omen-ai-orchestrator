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
