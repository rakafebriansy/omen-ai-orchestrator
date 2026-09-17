---
id: TICKET-74
title: Pembuatan Halaman Discovery Feed Pasar Keyakinan (/markets) & Tab Filter
status: Done
priority: High
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Discovery Feed (`app/markets/page.tsx`) adalah katalog penjelajahan pasar keyakinan publik.

Fitur utama halaman ini:
1. **Discovery Tabs**: Tab kurasi pasar: `Trending`, `Newest`, `Ending Soon`, `Most Volume`, dan `Confirmed`. (Sesuai brief, tidak ada algoritma For You / Following di V1).
2. **Search Bar**: Pencarian instan berbasis teks pernyataan belief, handle kreator, atau kategori.
3. **Grid Render**: Menampilkan daftar pasar menggunakan kartu `BeliefMarketCard` dengan layout grid responsif.
4. **Data Fetching**: Terhubung langsung ke endpoint `GET /api/markets` dengan query parameter `tab`, `search`, dan `category`.
5. **Loading & Empty State**: Menampilkan skeleton loader saat data dimuat dan ilustrasi empty state informatif jika tidak ada pasar yang sesuai.

> 🎨 **UI Style Preservation Note:**
> Desain tab pills dengan active highlight, search input box dengan ikon pencarian, skeleton loading shimmer, empty state container, dan tata letak grid kartu **WAJIB DIPERTAHANKAN** sesuai standar estetika antarmuka OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan halaman `app/markets/page.tsx` dan komponen filter `DiscoveryFilter.tsx`.
- [x] Menyediakan tab discovery: `Trending`, `Newest`, `Ending Soon`, `Most Volume`, dan `Confirmed`.
- [x] Mengambil data live dari endpoint `GET /api/markets` dengan penanganan state loading dan error yang mulus.
- [x] Mendukung input pencarian teks dan filter kategori.
- [x] Merender kartu `BeliefMarketCard` dalam grid responsif (1 kolom mobile, 2-3 kolom desktop).
- [x] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [x] Menyusun unit test pada `web/tests/markets-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/markets/page.tsx`
- `omen/web/components/DiscoveryFilter.tsx`
- `omen/web/tests/markets-page.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/markets-page.test.tsx` untuk pengujian discovery tabs (`Trending`, `Newest`, `Ending Soon`, `Most Volume`, `Confirmed`), filter kategori topic chips, input pencarian instan, dan rendering grid `BeliefMarketCard`.
  2. Mengimplementasikan komponen filter `omen/web/components/DiscoveryFilter.tsx` dan halaman `omen/web/app/markets/page.tsx` dengan preservasi styling OpenZeppelin dark mode, integrasi fetch `/api/markets`, skeleton loading shimmer, dan empty state.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/markets-page.test.tsx` -> 3/3 passing 100%) dan ESLint (`npx eslint app/markets/page.tsx components/DiscoveryFilter.tsx tests/markets-page.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/markets/page.tsx`
  - `omen/web/components/DiscoveryFilter.tsx`
  - `omen/web/tests/markets-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengombinasikan query parameter URL parsing dengan fallback sorting & filtering instan di sisi klien untuk memastikan fluiditas UX transisi filter tanpa flicker.
