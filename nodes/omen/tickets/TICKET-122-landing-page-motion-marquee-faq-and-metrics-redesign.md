---
id: TICKET-122
title: Redesign Landing Page and Full Website UI/UX (Polymarket Standard & Institutional Reference)
status: Done
priority: High
labels: [Frontend, UI/UX, LandingPage, Motion, FAQ, Marquee, DesignSystem, FullRedesign, PolymarketStyle]
---

# Deskripsi
Peningkatan kualitas antarmuka (*UI/UX Modernization & Polish*) secara menyeluruh pada Landing Page Omen (`omen/web/app/page.tsx`) dan seluruh halaman website Omen (`omen/web/app/markets/page.tsx`, `omen/web/app/market/[id]/page.tsx`, `omen/web/app/beliefs/page.tsx`, `omen/web/app/creators/page.tsx`, `omen/web/app/creator/[address]/page.tsx`, `omen/web/app/my-bets/page.tsx`, `omen/web/app/leaderboard/page.tsx`, `omen/web/app/admin/page.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`) berdasarkan *brief* revisi pengguna, referensi desain **Polymarket** ([polymarket.com](https://polymarket.com)), dan prototipe **HTML Omen Institutional Reference** yang diunggah untuk mengeliminasi segala bentuk kesan *AI slop/generik* dan menghadirkan estetika Web3 berstandar institusional (*Institutional Web3 / OpenZeppelin aesthetic*).

Peningkatan ini mencakup 7 area kunci:
1. **Motion UI & Micro-Animations:** Menambahkan animasi transisi GPU-accelerated yang mulus, ambient glowing gradients, hover-lift cards, and stagger entrance di seluruh section landing page.
2. **Infrastructure & Tech Stack Marquee:** Menambahkan komponen *infinite scrolling marquee* yang menampilkan stack ekosistem & teknologi Web3 Omen (Ethereum Sepolia, Robinhood Chain, Arbitrum, Chainlink Oracles, Viem/Wagmi, OpenRouter AI, Supabase, Foundry, Farcaster).
3. **Perluasan Section Landing Page (Featured Prediction Card, 5-Stage Flow, Live Activity Stream, & FAQ Accordion):** 
   - Menghadirkan **Interactive Featured Belief Card** dengan dual-track consensus (People vs Capital), signal gap pill, and live betting calculation simulator (referensi HTML).
   - Menghadirkan **5-Stage Protocol Lifecycle Flow** (*A belief appears ➔ The market opens ➔ The author confirms ➔ It resolves ➔ It is remembered*).
   - Menghadirkan **Live On-Chain Activity Stream & Creator Reputation Highlights**.
   - Menghadirkan **Interactive FAQ Accordion Section** dengan 5+ pertanyaan seputar Social Belief Markets, EIP-712 Signature, Pari-Mutuel Model, dan Resolusi Chainlink Oracle.
4. **Rich Mock Data Seeding untuk Trending Belief Markets:** Menyediakan *curated belief markets seed data* yang komprehensif pada komponen `TrendingMarketsTeaser.tsx` agar setiap tab kategori (`All`, `ETH`, `BTC`, `ARB`, `Macro`) menampilkan pasar aktif yang relevan tanpa *empty state* kosong saat penjelajahan.
5. **Redesign Stats Overview Metric Cards (Anti-AI Slop):** Merombak total 4 kartu metrik platform (`Total Protocol Volume`, `Active Markets`, `Total Beliefs`, `Verified Creators`) dengan tipografi berjenjang, angka tabular (`tabular-nums` / `font-mono`), glassmorphic sheen, badge indikator proporsional (`Sepolia & Robinhood`, `Escrow Verified`, `24/7 Staking`, `1.5% Fee Share`), dan penataan tata letak yang bersih, tegas, dan elegan.
6. **Website-Wide Institutional UI/UX Modernization (Polymarket & HTML Reference):**
   - Menyelaraskan seluruh komponen kartu pasar (`omen/web/components/BeliefMarketCard.tsx`, `omen/web/components/MarketCard.tsx`) dengan tombol split odds Agree/Disagree (`Agree 72%` / `Disagree 28%`), progress bar probabilitas terintegrasi, dan pill volume/trader yang tajam.
   - Merapikan halaman Discovery Feed (`omen/web/app/markets/page.tsx`), Market Detail Multi-Panel (`omen/web/app/market/[id]/page.tsx`), Beliefs Feed (`omen/web/app/beliefs/page.tsx`), Creators Directory (`omen/web/app/creators/page.tsx`), Creator Profile (`omen/web/app/creator/[address]/page.tsx`), My Bets (`omen/web/app/my-bets/page.tsx`), Leaderboard (`omen/web/app/leaderboard/page.tsx`), dan Admin Portal (`omen/web/app/admin/page.tsx`) agar seragam mengadopsi estetika Polymarket / HTML Reference yang bersih, berbobot, dan beresolusi tinggi di mode gelap & terang.
7. **Unified Single-Page Navigation & Seamless Section Anchors (omen.html Standard):**
   - Menyatukan seluruh navigasi utama (`Markets`, `Beliefs`, `Creators`, `Activity`) yang sebelumnya terpisah menjadi satu halaman terpadu di halaman utama (`omen/web/app/page.tsx` dengan anchor `#markets`, `#creators`, `#activity`, `#how-it-works`, `#faq`) seperti pada arsitektur `omen.html`.
   - Menyesuaikan tautan Navbar dan navigasi mobile agar menggunakan smooth anchor scroll (`#markets`, `#creators`, `#activity`, `#how-it-works`) saat berada di homepage, serta fallback route kanonikal (`/#markets`, dst.) saat berada di sub-halaman.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] **Motion UI Enhancement:** Landing page memiliki efek animasi masuk (*stagger entrance*), glow ambient subtle, dan hover interactions yang terasa hidup dan responsif di tema gelap & terang.
- [x] **Infrastructure Tech Stack Marquee:** Dibuat komponen baru `InfraMarquee.tsx` dengan animasi *infinite marquee scrolling* yang menampilkan logo/nama stack: Ethereum Sepolia, Robinhood Chain, Arbitrum, Chainlink, Viem, Wagmi, OpenRouter, Supabase, Foundry, Farcaster.
- [x] **Extended Landing Sections (Featured Card, Flow, Activity, & FAQ):** Dibuat komponen `FeaturedBeliefHero.tsx`, `ProtocolFlow.tsx`, `LandingActivityStream.tsx`, dan `LandingFAQ.tsx` yang setia pada struktur prototipe HTML referensi.
- [x] **Rich Seed Data pada Trending Markets:** Seluruh tab filter (`All`, `ETH`, `BTC`, `ARB`, `Macro`) pada `TrendingMarketsTeaser.tsx` terisi data pasar berbobot dan interaktif.
- [x] **Premium Stats Overview Cards Redesign:** Komponen `StatsOverview.tsx` dirombak total dengan visual kelas institusional, tata letak data yang terorganisir rapi, kontras tajam di mode gelap & terang, dan bebas dari tampilan kaku/berantakan.
- [x] **Full Website UI/UX Alignment:** Seluruh halaman utama (`/markets`, `/market/[id]`, `/beliefs`, `/creators`, `/creator/[address]`, `/my-bets`, `/leaderboard`, `/admin`, `Navbar`, `Footer`) diselaraskan ke desain institusional Polymarket & HTML reference.
- [x] **Unified Single-Page Navigation:** Seluruh navigasi Navbar dan section landing page terhubung dalam satu halaman terpadu (`#markets`, `#creators`, `#activity`, `#how-it-works`, `#faq`) dengan smooth scrolling.
- [x] **Testing & Quality:** Seluruh test suites Vitest (`npm test`) lulus 100% (77/77 suites, 403/403 tests), `npx tsc --noEmit` lolos 0 error, dan 100% patuh pada Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/landing/StatsOverview.tsx`
- `omen/web/components/landing/TrendingMarketsTeaser.tsx`
- `omen/web/components/landing/InfraMarquee.tsx` [NEW]
- `omen/web/components/landing/FeaturedBeliefHero.tsx` [NEW]
- `omen/web/components/landing/ProtocolFlow.tsx` [NEW]
- `omen/web/components/landing/LandingActivityStream.tsx` [NEW]
- `omen/web/components/landing/LandingFAQ.tsx` [NEW]
- `omen/web/components/BeliefMarketCard.tsx`
- `omen/web/components/MarketCard.tsx`
- `omen/web/components/Navbar.tsx`
- `omen/web/components/Footer.tsx`
- `omen/web/app/page.tsx`
- `omen/web/app/markets/page.tsx`
- `omen/web/app/market/[id]/page.tsx`
- `omen/web/app/beliefs/page.tsx`
- `omen/web/app/creators/page.tsx`
- `omen/web/app/creator/[address]/page.tsx`
- `omen/web/app/my-bets/page.tsx`
- `omen/web/app/leaderboard/page.tsx`
- `omen/web/app/admin/page.tsx`
- `omen/web/app/globals.css`
- `omen/web/tests/landing.test.tsx`
- `omen/web/tests/navbar.test.tsx`
- `omen/web/tests/footer.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menambahkan utility CSS `@keyframes marquee`, `@keyframes feedSlideIn`, `.animate-marquee`, `.animate-feed-slide`, `.tnum`, dan `html { scroll-behavior: smooth }` pada `omen/web/app/globals.css`.
  2. Mengimplementasikan komponen baru `InfraMarquee.tsx` dengan auto-scrolling loop menampilkan ekosistem Web3 Omen (Ethereum Sepolia, Robinhood Chain, Arbitrum, Chainlink, Viem, Wagmi, OpenRouter, Supabase, Foundry, Farcaster).
  3. Mengimplementasikan komponen `FeaturedBeliefHero.tsx` yang interaktif dengan dynamic payout calculation simulator, dual-track consensus bar (People vs Capital), dan visual EIP-712 status badge.
  4. Mengimplementasikan komponen `ProtocolFlow.tsx` dengan visualisasi interaktif 5-tahap siklus hidup protokol prediksi belief.
  5. Mengimplementasikan `LandingActivityStream.tsx` yang menyatukan high-conviction creator spotlight (`@TraderX`) dengan simulasi live transaction ticker on-chain.
  6. Mengimplementasikan komponen interaktif `LandingFAQ.tsx` dengan accordion 6 pertanyaan mendalam seputar arsitektur sosial, EIP-712, dan resolusi oracle.
  7. Merombak total `StatsOverview.tsx` menjadi 4 kartu metrik presisi tinggi berstandar institusional dengan tabular figures (`tabular-nums font-mono`) dan badge proporsional tanpa AI slop.
  8. Menambahkan rich seed mock data di `TrendingMarketsTeaser.tsx` untuk tab `All`, `ETH`, `BTC`, `ARB`, `Macro` serta menyelaraskan tombol odds split style Polymarket.
  9. Menyelaraskan seluruh kartu pasar (`BeliefMarketCard.tsx`, `MarketCard.tsx`) ke gaya Polymarket split Yes/No & Agree/Disagree buttons, probability progress bar, dan metadata chip tajam.
  10. Menata `Navbar.tsx` dan `Footer.tsx` untuk mendukung single-page smooth scroll anchor navigation (`/#markets`, `/#creators`, `/#activity`, `/#how-it-works`, `/#faq`).
  11. Mengintegrasikan seluruh komponen dalam `omen/web/app/page.tsx` sesuai arsitektur referensi `omen.html`.
  12. Menyesuaikan dan memvalidasi unit test suites (`landing.test.tsx`, `navbar.test.tsx`, `footer.test.tsx`), memastikan 77 test suites lulus 100% (403 tests) dan TypeScript 0 error.
  13. Menjalankan `graphify update` pada root repositori `omen` untuk menyinkronkan graph context kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/globals.css`
  - `omen/web/components/landing/InfraMarquee.tsx` [NEW]
  - `omen/web/components/landing/FeaturedBeliefHero.tsx` [NEW]
  - `omen/web/components/landing/ProtocolFlow.tsx` [NEW]
  - `omen/web/components/landing/LandingActivityStream.tsx` [NEW]
  - `omen/web/components/landing/LandingFAQ.tsx` [NEW]
  - `omen/web/components/landing/StatsOverview.tsx`
  - `omen/web/components/landing/TrendingMarketsTeaser.tsx`
  - `omen/web/components/landing/HeroSection.tsx`
  - `omen/web/components/BeliefMarketCard.tsx`
  - `omen/web/components/MarketCard.tsx`
  - `omen/web/components/Navbar.tsx`
  - `omen/web/components/Footer.tsx`
  - `omen/web/app/page.tsx`
  - `omen/web/tests/landing.test.tsx`
  - `omen/web/tests/navbar.test.tsx`
  - `omen/web/tests/footer.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Seluruh kode `.ts` dan `.tsx` mematuhi Zero-Comment Policy 100%.
  - Navigasi satu halaman menggunakan anchor ID eksplisit (`#markets`, `#creators`, `#activity`, `#how-it-works`, `#faq`) yang kompatibel baik saat diakses langsung dari root maupun saat berpindah dari sub-halaman lain.
