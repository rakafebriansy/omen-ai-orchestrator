---
id: TICKET-12
title: Pembuatan Komponen Filter Kategori Pasar Prediksi
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun bar navigasi filter kategori dan pengurutan pasar prediksi di `omen/web/components/MarketCategoryFilter.tsx`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`MarketCategoryFilter.tsx`)
1. **Pill Kategori Horizontal:**
   - Tombol tab: "All Markets", "Trending", "Crypto Narratives", "Meme Tokens", "Closing Soon", "Resolved".
   - *State Aktif:* `bg-accent-navy text-white px-4 py-2 rounded-lg font-semibold text-sm shadow-xs`.
   - *State Inaktif:* `bg-white border border-border-subtle text-text-muted hover:text-accent-navy hover:bg-bg-subtle px-4 py-2 rounded-lg font-medium text-sm transition-all`.
2. **Pencarian dan Urutan (Search dan Sort Controls):**
   - Input teks pencarian judul pasar dengan ikon kaca pembesar.
   - Dropdown pengurutan: "Highest Pool", "Ending Soonest", "Newest".

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Pill filter kategori dapat diklik dengan indikator aktif yang tegas.
- [ ] Input teks pencarian memicu callback pencarian pasar.
- [ ] Dropdown pengurutan mengubah parameter sorting pasar.
- [ ] Unit test komponen MarketCategoryFilter lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/MarketCategoryFilter.tsx`
- `omen/web/tests/market-filter.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
