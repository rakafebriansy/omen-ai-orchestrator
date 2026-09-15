---
id: TICKET-14
title: Pembuatan Halaman Katalog Pasar Prediksi
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman katalog utama pasar prediksi di `omen/web/app/predictions/page.tsx` yang memuat filter kategori, bar pencarian, grid kartu pasar `MarketCard`, dan skeleton loading state.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Halaman (`app/predictions/page.tsx`)
1. **Header Halaman:**
   - Judul H1: "Prediction Markets" (`text-3xl sm:text-4xl font-extrabold text-accent-navy tracking-tight`).
   - Subjudul ringkas dan counter total pasar aktif.
2. **Kontrol Filter dan Pencarian:**
   - Merender komponen `MarketCategoryFilter`.
3. **Grid Katalog Pasar:**
   - Layout grid: `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 my-8`.
   - Render daftar komponen `MarketCard`.
4. **Skeleton Loading State:**
   - Kartu placeholder beranimasi pulse saat data sedang dimuat.
5. **Empty State:**
   - Tampilan jika tidak ada pasar yang sesuai dengan kata kunci pencarian.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Halaman merender filter kategori dan grid kartu pasar prediksi secara responsif.
- [ ] Skeleton loader tampil saat kondisi loading aktif.
- [ ] Tersedia tampilan fallback saat hasil pencarian nihil.
- [ ] Unit test halaman predictions berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/predictions/page.tsx`
- `omen/web/tests/predictions-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
