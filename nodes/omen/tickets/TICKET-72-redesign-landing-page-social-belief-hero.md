---
id: TICKET-72
title: Redesign Landing Page dengan Hero Social Belief & Live Market Feeds
status: Done
priority: High
labels: [Frontend, UI, Landing]
---

# Deskripsi
Halaman utama (`app/page.tsx`) perlu disesuaikan agar menyampaikan proposisi nilai baru OMEN V1: *"THE INTERNET IS FULL OF OPINIONS. OMEN GIVES THEM A MARKET."*

Halaman ini akan menyajikan:
1. **Hero Section**: Headline tajam, subheadline penjelas transformasi social belief menjadi pasar terverifikasi on-chain, serta tombol CTA ganda: "Explore Markets" (`/markets`) dan "Submit Belief" (`/create`).
2. **Trending Beliefs Section**: Menampilkan cuplikan pasar-pasar keyakinan terhangat menggunakan komponen `BeliefMarketCard` yang disuplai dari live API.
3. **Platform Metrics Section**: Menampilkan ringkasan metrik Total Volume ETH, Active Markets, Total Beliefs Indexed, dan Verified Creators.
4. **Pembersihan Modul Lama**: Menghapus referensi teaser Quests/Daily Farming dari landing page.

> 🎨 **UI Style Preservation Note:**
> Seluruh sistem desain visual yang telah dibangun — meliputi tema OpenZeppelin dark mode, palet warna gelap dengan aksen emerald/rose, efek glassmorphism, tipografi font, gradient glow, button styles, dan micro-animations — **WAJIB DIPERTAHANKAN**. Jangan melakukan perombakan tema styling global atau mengganti visual token Tailwind dari awal.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memperbarui hero headline, sub-headline, dan tombol CTA pada `app/page.tsx` atau `components/landing/HeroSection.tsx`.
- [x] Mengganti komponen teaser lama dengan section "Trending Beliefs" yang merender `BeliefMarketCard`.
- [x] Menghubungkan kartu metrik platform (`StatsOverview.tsx`) ke data agregasi V1 (Total Volume, Active Markets, Total Beliefs, Verified Creators).
- [x] Menghapus referensi Quests Teaser dari tampilan halaman utama.
- [x] Mempertahankan style UI, tema dark mode, dan responsivitas mobile/desktop.
- [x] Menyusun/memperbarui unit test di `web/tests/landing.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/page.tsx`
- `omen/web/components/landing/HeroSection.tsx`
- `omen/web/components/landing/StatsOverview.tsx`
- `omen/web/components/landing/TrendingMarketsTeaser.tsx`
- `omen/web/components/landing/OnboardingJourney.tsx`
- `omen/web/tests/landing.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/landing.test.tsx` untuk pengujian hero section headline & badge dual-testnet, tombol CTA ganda (`/markets` & `/create`), 4 metrik platform V1, grid feed `BeliefMarketCard` dinamis, dan 3-step Social Belief onboarding journey.
  2. Memperbarui `HeroSection.tsx`, `StatsOverview.tsx`, `TrendingMarketsTeaser.tsx`, `OnboardingJourney.tsx`, dan `app/page.tsx` untuk menghapus komponen Quests lama dan menampilkan antarmuka Social Belief Protocol V1 dengan tema OpenZeppelin dark mode dan aksen emerald.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/landing.test.tsx` -> 5/5 passing 100%) dan ESLint (`npx eslint app/page.tsx components/landing/... tests/landing.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/page.tsx`
  - `omen/web/components/landing/HeroSection.tsx`
  - `omen/web/components/landing/StatsOverview.tsx`
  - `omen/web/components/landing/TrendingMarketsTeaser.tsx`
  - `omen/web/components/landing/OnboardingJourney.tsx`
  - `omen/web/tests/landing.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengeliminasi dependensi teaser gamifikasi usang (Quests) dari landing page dan mengalihkan fokus utama ke konversi keyakinan sosial (*social conviction*) dan likuiditas pasar.
