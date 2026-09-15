---
id: TICKET-04
title: Pembuatan Halaman Landing dan Statistik Platform
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman beranda (Landing Page) berestetika OpenZeppelin Institutional Web3 di `omen/web` pada rute `app/page.tsx`. Halaman ini berfungsi sebagai etalase utama yang memperkenalkan protokol Omen, menampilkan statistik metrik ekosistem secara langsung, menjelaskan pilar ganda platform (Prediction Market dan Quest Farming), serta mengarahkan pengguna untuk mulai berpartisipasi.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### 1. Hero Section (`HeroSection.tsx`)
- **Badge Pengantar:** Pill badge di atas judul `bg-primary-blue-soft text-primary-blue text-xs font-mono font-semibold px-3 py-1 rounded-full border border-primary-blue/20` bertuliskan "Decentralized Prediction Markets dan Gamified Points".
- **Headline Utama (Display H1):** `text-4xl sm:text-5xl lg:text-6xl font-extrabold tracking-tight text-accent-navy leading-tight`.
- **Subheadline:** `text-lg sm:text-xl text-text-muted max-w-2xl mx-auto leading-relaxed mt-4`.
- **Call-to-Action (CTA) Group:**
  - Tombol Primer: "Explore Markets" (`bg-primary-blue text-white hover:bg-primary-blue-hover px-6 py-3 rounded-lg font-semibold shadow-sm transition-all`).
  - Tombol Sekunder: "Earn Quest Points" (`border border-border-subtle bg-white text-text-primary hover:bg-bg-subtle px-6 py-3 rounded-lg font-semibold transition-all`).

### 2. Stats Overview Cards (`StatsOverview.tsx`)
- **Grid Kontainer:** `grid grid-cols-2 lg:grid-cols-4 gap-4 sm:gap-6 my-12`.
- **Kartu Metrik (`bg-white border border-border-subtle rounded-xl p-6 shadow-sm`):**
  1. **Total Value Locked / Bet Pool:** Nilai nominal ETH terkunci (contoh: "142.50 ETH").
  2. **Active Predictions:** Jumlah pasar yang sedang aktif berjalan (contoh: "24 Markets").
  3. **Total Points Distributed:** Akumulasi poin reward yang telah dibagikan (contoh: "1,250,000 PTS").
  4. **Active Bettors / Wallets:** Jumlah pengguna unik yang terhubung (contoh: "3,890 Wallets").
- **Tipografi Nilai:** `text-2xl sm:text-3xl font-extrabold font-mono text-accent-navy`.

### 3. Pilar Ganda Protokol (`FeaturePillars.tsx`)
- **Dua Kartu Fitur Berdampingan (`grid grid-cols-1 md:grid-cols-2 gap-8 my-10`):**
  - **Pilar 1 (Prediction Market):** Kartu penjelasan pasar prediksi dua arah (Yes/No) non-kustodian bertenaga smart contract Arbitrum Sepolia.
  - **Pilar 2 (Quest dan Streak Engine):** Kartu penjelasan mekanisme farming poin harian tanpa biaya gas fee melalui database Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Hero banner merender judul Display H1, subjudul, dan dua tombol CTA dengan tautan rute yang tepat.
- [ ] Komponen StatsOverview merender 4 kartu metrik dengan tipografi font-mono yang presisi.
- [ ] Seksi FeaturePillars menjelaskan pilar ganda protokol dengan tata letak visual yang seimbang.
- [ ] Memenuhi rasio kontras WCAG 2.1 AA dan sepenuhnya responsif dari mobile hingga desktop.
- [ ] Unit test komponen landing page berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/page.tsx`
- `omen/web/components/HeroSection.tsx`
- `omen/web/components/StatsOverview.tsx`
- `omen/web/components/FeaturePillars.tsx`
- `omen/web/tests/landing.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
