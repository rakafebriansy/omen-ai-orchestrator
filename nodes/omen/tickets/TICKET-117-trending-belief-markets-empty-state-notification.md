---
id: TICKET-117
title: Add Empty State Notification for Trending Belief Markets on Landing Page
status: Done
priority: Medium
labels: [Frontend, UI, LandingPage, EmptyState]
---

# Deskripsi
Menambahkan UI pemberitahuan *empty state* pada section "Trending Belief Markets" di halaman beranda (`/` via `web/components/landing/TrendingMarketsTeaser.tsx`) ketika tidak ada pasar belief yang ditemukan atau saat filter kategori tidak menghasilkan data.

### Akar Masalah:
- Komponen `TrendingMarketsTeaser.tsx` sebelumnya hanya merender grid kosong `<div className="grid grid-cols-1 md:grid-cols-2 gap-4"></div>` tanpa pesan informatif atau call-to-action saat `filteredMarkets.length === 0`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Tampilkan *empty state card* berdesain premium dengan ikon info, judul *"No trending belief markets found"*, deskripsi kontekstual berdasarkan tab aktif, dan tombol CTA *"Submit New Belief ↗"*.
- [x] Inisialisasi state `markets` secara murni dari data API tanpa mengandalkan mock data statis yang membingungkan.
- [x] Tambahkan unit test di `web/tests/landing.test.tsx` untuk memverifikasi tampilan pesan kosong saat API mengembalikan array kosong.
- [x] Pastikan seluruh test Vitest (77 test suites, 396 unit tests) lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `web/components/landing/TrendingMarketsTeaser.tsx`
- `web/tests/landing.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menambahkan komponen *empty state* pada `web/components/landing/TrendingMarketsTeaser.tsx` yang responsif terhadap dark/light mode dan filter tab kategori.
  2. Menghapus konstanta `DEFAULT_MARKETS` agar murni mengonsumsi data dari endpoint `/api/markets`.
  3. Menambahkan unit test di `web/tests/landing.test.tsx` untuk menguji kondisi `markets: []`.
  4. Menjalankan `npm test` untuk memverifikasi 396 tests lulus 100%.
  5. Menjalankan `graphify update` untuk menyinkronkan AST Knowledge Graph.
- **Ringkasan File Terpengaruh:**
  - `web/components/landing/TrendingMarketsTeaser.tsx`
  - `web/tests/landing.test.tsx`
