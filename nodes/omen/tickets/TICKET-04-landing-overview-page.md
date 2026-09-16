---
id: TICKET-04
title: Pembuatan Halaman Landing Dual Theme Dark dan Light Emerald
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman beranda (Landing Page) berestetika Dual Theme (**Dark Emerald Mode** dan **Light Emerald Mode**) di `omen/web` pada rute `app/page.tsx` yang disesuaikan secara khusus untuk pilar ekosistem Web3 Omen: Betting, Airdrop, Crypto, Gamification, dan Quest. Halaman ini berfungsi sebagai etalase utama yang memperkenalkan protokol Omen dengan dukungan perpindahan tema interaktif, sistem gradasi bertingkat, aset render 3D fotorealistik, dan kartu-kartu ekosistem yang adaptif.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### 1. Hero Section (`HeroSection.tsx`)
- **Shared Structural System:** Kontainer rounded-3xl (`border-radius: 24px`) berbingkai rapi dengan breathing room dan sticky header inset.
- **Dark Emerald Mode (Centered Stack):**
  - Background `#030906` dengan glowing emerald seam line (`linear-gradient(90deg, transparent, #10B981, transparent)`).
  - Headline Display H1: `clamp(42px, 7.5vw, 96px)` font-black text-white.
  - Primary CTA: Deep emerald gradient (`linear-gradient(180deg, #34D399 0%, #047857 100%)`) dengan soft emerald glow shadow (`box-shadow: 0 0 40px rgba(16, 185, 129, 0.45)`).
  - 3D Visual Asset: Full-bleed `/images/hero-dark-emerald.jpg` menampilkan pita liquid metal ber-rim light hijau zamrud.
- **Light Emerald Mode (Left-Aligned Split Layout):**
  - Layered CSS gradient multi-stop (radial mint-emerald bloom di titik 78% 55% dan 100% 100% serta linear 160deg).
  - Kolom kiri (~48%): Headline 2-baris `clamp(38px, 5.2vw, 68px)`, subteks charcoal-green, dan tombol dark forest `#10221A` dengan icon `ArrowRight`.
  - Kolom kanan (~50%): Objek 3D Glossy Emerald Turbine Sculpture (`/images/hero-light-emerald.png`) melayang tepat di atas pendaran radial mint bloom.

### 2. Header dan Theme Switcher (`Navbar.tsx` dan `ThemeProvider.tsx`)
- Sticky header inset dengan backdrop blur dan switch toggle interaktif Light Mode / Dark Mode.
- Logo Omen berbobot 800, badge Testnet Arbitrum Sepolia, menu navigasi desktop dan responsive drawer mobile.

### 3. Stats Overview Cards (`StatsOverview.tsx`)
- 4 kartu metrik adaptif (TVL 148.50 ETH, 24 Markets, 1,420,000 PTS, 4,120 Wallets).

### 4. Pilar Ganda Protokol (`FeaturePillars.tsx`)
- Pilar I: Non-Custodial Binary Betting di Arbitrum Sepolia.
- Pilar II: Gamified Daily Quests dan Airdrop Points Engine.

### 5. Seksi Tambahan Ekosistem Web3
- `TrendingMarketsTeaser.tsx`: Cuplikan live odds Yes/No.
- `QuestsTeaser.tsx`: Kalender 7-day streak dan active quest cards.
- `AirdropBanner.tsx`: Banner kampanye Season 1 Airdrop Points.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Hero section mendukung varian tema ganda (Dark Emerald centered stack dan Light Emerald left-aligned split).
- [x] Aset visual 3D photorealistic render untuk Dark Emerald dan Light Emerald terpasang presisi.
- [x] Background gradient Light Mode diimplementasikan dengan multi-layer CSS radial dan linear gradients.
- [x] ThemeProvider dan Navbar theme toggle berfungsi mulus untuk beralih mode.
- [x] Memenuhi rasio kontras WCAG 2.1 AA dan responsif mobile-first.
- [x] Unit test komponen landing page berhasil lulus pengujian Vitest (100% passing).

## Target Lingkup File (Affected Files)
- `omen/web/app/page.tsx`
- `omen/web/app/layout.tsx`
- `omen/web/app/globals.css`
- `omen/web/components/ThemeProvider.tsx`
- `omen/web/components/Navbar.tsx`
- `omen/web/components/Footer.tsx`
- `omen/web/components/landing/HeroSection.tsx`
- `omen/web/components/landing/StatsOverview.tsx`
- `omen/web/components/landing/FeaturePillars.tsx`
- `omen/web/components/landing/TrendingMarketsTeaser.tsx`
- `omen/web/components/landing/QuestsTeaser.tsx`
- `omen/web/components/landing/OnboardingJourney.tsx`
- `omen/web/components/landing/AirdropBanner.tsx`
- `omen/web/public/images/hero-dark-emerald.jpg`
- `omen/web/public/images/hero-light-emerald.png`
- `omen/web/public/icons/btc.webp`
- `omen/web/public/icons/eth.webp`
- `omen/web/public/icons/arb.webp`
- `omen/web/public/icons/hot.webp`
- `omen/web/public/icons/macro.webp`
- `omen/web/tests/landing.test.tsx`
- `omen/web/tests/navbar.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menghasilkan dua aset 3D render fotorealistik kualitas tinggi: `hero-dark-emerald.jpg` (liquid metal waves ber-rim light emerald) dan `hero-light-emerald.png` (turbin kristal zamrud berlatar transparan).
  2. Mengimplementasikan `ThemeProvider.tsx` dan `globals.css` dengan token warna Dark Emerald (`#030906`, `#0A0F0C`, `#34D399`, `#047857`) dan Light Emerald (`#CFF3E2`, `#A9EAC9`, `#0B1F16`, `#10221A`, `#0E7A4E`), serta layered multi-stop gradient.
  3. Mengimplementasikan komponen `HeroSection.tsx` dengan dukungan prop `theme="dark" | "light"` dan layout ganda (Centered Stack untuk Dark Mode dan Left-Aligned Split untuk Light Mode).
  4. Memperbarui `Navbar.tsx` dengan theme toggle button dan styling adaptif.
  5. Menyelaraskan seluruh sub-komponen landing page (`StatsOverview.tsx`, `FeaturePillars.tsx`, `TrendingMarketsTeaser.tsx`, `QuestsTeaser.tsx`, `AirdropBanner.tsx`, `Footer.tsx`) agar adaptif terhadap tema aktif.
  6. Memperbarui unit testing di `tests/landing.test.tsx` dan `tests/navbar.test.tsx` (23 tests passing 100% pada Vitest).
  8. Mentransformasi seluruh grid simetris ("AI-slop") menjadi susunan Asymmetric Bento Architecture dan Variasi Kartu Informasi Kaya.
  9. Mentransformasi landing page dengan bahasa desain pertukaran global (**Bitget.com** style):
     - `StatsOverview.tsx`: Live Exchange Ticker Bar & Protocol Metric Strip dengan garis batas 1px dan pulse status.
     - `TrendingMarketsTeaser.tsx`: Interactive Tabbed Live Markets Table dengan tab filter kategori (`Hot`, `Crypto`, `L2`, `Macro`), meter probabilitas YES/NO, volume pool, dan tombol quick-bet instan di tiap baris.
     - `FeaturePillars.tsx`: Split Product Terminal Showcases dengan kalkulator Trading Slip Simulator interaktif & Streak Multiplier Vault.
     - `QuestsTeaser.tsx`: Task Center & Rewards Hub layout dengan 7-day streak progress dan table task list.
     - `OnboardingJourney.tsx`: [NEW] 3-Step User Journey Sequence (`01`, `02`, `03`) terhubung garis alur.
  10. Mengunduh aset PNG ikon kripto resmi (Bitcoin, Ethereum, Arbitrum, Hot Flame, Macro Globe), mengonversinya ke format WebP terkompresi optimal dengan transparansi penuh (`cwebp -q 95 -alpha_q 100`), dan mengintegrasikannya dengan komponen `next/image` pada `TrendingMarketsTeaser.tsx`.
  11. Memperbarui unit testing (24 tests passing 100% pada Vitest) dan memverifikasi Zero-Comment Policy secara menyeluruh.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/page.tsx` [Updated]
  - `omen/web/app/layout.tsx` [Updated]
  - `omen/web/app/globals.css` [Updated]
  - `omen/web/components/ThemeProvider.tsx` [Created]
  - `omen/web/components/Navbar.tsx` [Updated]
  - `omen/web/components/Footer.tsx` [Updated]
  - `omen/web/components/landing/HeroSection.tsx` [Updated]
  - `omen/web/components/landing/StatsOverview.tsx` [Updated]
  - `omen/web/components/landing/FeaturePillars.tsx` [Updated]
  - `omen/web/components/landing/TrendingMarketsTeaser.tsx` [Updated]
  - `omen/web/components/landing/QuestsTeaser.tsx` [Updated]
  - `omen/web/components/landing/OnboardingJourney.tsx` [Created]
  - `omen/web/components/landing/AirdropBanner.tsx` [Updated]
  - `omen/web/public/images/hero-dark-emerald.jpg` [Created]
  - `omen/web/public/images/hero-light-emerald.png` [Created]
  - `omen/web/public/icons/btc.webp` [Created]
  - `omen/web/public/icons/eth.webp` [Created]
  - `omen/web/public/icons/arb.webp` [Created]
  - `omen/web/public/icons/hot.webp` [Created]
  - `omen/web/public/icons/macro.webp` [Created]
  - `omen/web/tests/landing.test.tsx` [Updated]
  - `omen/web/tests/navbar.test.tsx` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Arsitektur tema ganda Dark Emerald dan Light Emerald menyatu secara terstruktur dengan sistem token Tailwind CSS dan tetap mempertahankan nuansa institusional Web3 Arbitrum Sepolia.
  - Bahasa desain Bitget Exchange (Tabbed Data Tables, Ticker Bar, Split Simulation Terminals, 3-Step Onboarding) menghilangkan kejenuhan "card fatigue" dan menghadirkan pengalaman trading & quest Web3 berdensitas data tinggi tanpa mengubah konten aslinya.
  - Aset ikon resmi WebP memberikan kejernihan visual maksimal dan bobot payload yang sangat ringan.

