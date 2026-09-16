---
id: TICKET-72
title: Redesign Landing Page dengan Hero Social Belief & Live Market Feeds
status: Todo
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
- [ ] Memperbarui hero headline, sub-headline, dan tombol CTA pada `app/page.tsx` atau `components/landing/HeroSection.tsx`.
- [ ] Mengganti komponen teaser lama dengan section "Trending Beliefs" yang merender `BeliefMarketCard`.
- [ ] Menghubungkan kartu metrik platform (`StatsOverview.tsx`) ke data agregasi V1 (Total Volume, Active Markets, Total Beliefs, Verified Creators).
- [ ] Menghapus referensi Quests Teaser dari tampilan halaman utama.
- [ ] Mempertahankan style UI, tema dark mode, dan responsivitas mobile/desktop.
- [ ] Menyusun/memperbarui unit test di `web/tests/landing.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/page.tsx`
- `omen/web/components/landing/HeroSection.tsx`
- `omen/web/components/landing/StatsOverview.tsx`
- `omen/web/components/landing/TrendingMarketsTeaser.tsx`
- `omen/web/tests/landing.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
