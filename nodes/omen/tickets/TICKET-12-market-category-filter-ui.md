---
id: TICKET-12
title: Pembuatan Komponen Filter Kategori Pasar Prediksi
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun bar navigasi filter kategori dan pengurutan pasar prediksi di `omen/web/components/MarketCategoryFilter.tsx`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`MarketCategoryFilter.tsx`)
1. **Pill Kategori Horizontal:**
   - Tombol tab: "All Markets", "Trending", "Crypto Narratives", "Meme Tokens", "Closing Soon", "Resolved".
   - *State Aktif:* `bg-emerald-600 text-white dark:bg-emerald-500 dark:text-zinc-950 px-4 py-2 rounded-lg font-semibold text-sm shadow-xs`.
   - *State Inaktif:* `bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 text-zinc-600 dark:text-zinc-400 hover:text-emerald-600 dark:hover:text-emerald-400 hover:bg-zinc-50 dark:hover:bg-zinc-800/60 px-4 py-2 rounded-lg font-medium text-sm transition-all`.
2. **Pencarian dan Urutan (Search dan Sort Controls):**
   - Input teks pencarian judul pasar dengan ikon kaca pembesar SVG dan tombol reset clear pencarian.
   - Dropdown pengurutan: "Highest Pool", "Ending Soonest", "Newest".

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Pill filter kategori dapat diklik dengan indikator aktif yang tegas.
- [x] Input teks pencarian memicu callback pencarian pasar.
- [x] Dropdown pengurutan mengubah parameter sorting pasar.
- [x] Unit test komponen MarketCategoryFilter lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/MarketCategoryFilter.tsx`
- `omen/web/tests/market-filter.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat `MarketCategoryFilter.tsx` dengan daftar kategori lengkap (*All Markets, Trending, Crypto Narratives, Meme Tokens, Closing Soon, Resolved*), search text input interaktif dengan tombol reset, dan dropdown sorting opsi pool/waktu.
  2. Menyusun test suite `market-filter.test.tsx` dengan 5 skenario pengujian komprehensif menguji rendering pills, state aktif, triggering `onSelectCategory`, typing & clearing search input `onSearchChange`, sorting dropdown `onSortChange`, dan rendering badges jumlah market.
  3. Memverifikasi seluruh pengujian Vitest (total 60/60 tests pass 100%), type check TypeScript bersih, dan kepatuhan penuh Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/MarketCategoryFilter.tsx` [Created]
  - `omen/web/tests/market-filter.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-12-market-category-filter-ui.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan struktur flexbox responsif dengan horizontal scrolling halus pada kategori pill untuk perangkat mobile (`overflow-x-auto scrollbar-none`), serta layout flex row pada desktop untuk search input dan sort dropdown.
  - Komponen mendukung opsional `marketCounts` dictionary untuk merender badge jumlah item per kategori secara dinamis.
