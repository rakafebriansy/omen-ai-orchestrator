---
id: TICKET-61
title: Integrasi Pure Dynamic Feed Pasar Prediksi & Sinkronisasi Filter Kategori
status: Done
priority: High
labels: [Frontend, Backend, Feature, Supabase, Predictions]
---

# Deskripsi
Halaman `app/predictions/page.tsx` masih menyimpan dataset statis `MOCK_MARKETS` (baris 11–101) sebagai state awal dan fallback pencarian (baris 238). Ketika database Supabase kosong atau sedang loading, aplikasi dapat merender pasar-pasar tiruan tersebut alih-alih menampilkan loading skeleton atau empty state.

Tiket ini bertujuan untuk menghapus `MOCK_MARKETS`, memastikan pengambilan data pasar murni dinamis dari `GET /api/markets`, menyinkronkan hitungan kuantitas pada tab kategori (`All`, `Crypto`, `L2`, `Trending`, `Meme`, `Closing Soon`, `Resolved`) secara akurat dari basis data, serta mengintegrasikan modal taruhan dengan data pasar nyata.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menghapus array statis `MOCK_MARKETS` pada `omen/web/app/predictions/page.tsx`.
- [x] Mengambil seluruh katalog pasar prediksi langsung dari `GET /api/markets` tanpa fallback array tiruan.
- [x] Mengkalkulasi jumlah total pasar per kategori secara dinamis dari data live Supabase.
- [x] Menyediakan *skeleton loading state* yang rapi saat data pasar sedang di-fetch, dan tampilan *empty state* yang informatif jika tidak ada pasar ditemukan.
- [x] Menghubungkan pembukaan modal taruhan (`BettingModal`) langsung ke ID pasar dan rasio odds pool nyata.
- [x] Seluruh unit tests Vitest di `omen/web` lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/predictions/page.tsx`
- `omen/web/tests/predictions-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan test suite TDD pada `web/tests/predictions-page.test.tsx` untuk memvalidasi fetching katalog pasar live dari `GET /api/markets`, kategori filtering dinamis, search filtering, empty state reset, dan dialog konfirmasi taruhan.
  2. Menghapus dataset statis `MOCK_MARKETS` dari `web/app/predictions/page.tsx`.
  3. Mengintegrasikan komponen `MarketCategoryFilter` dan `MarketCard` secara terpadu tanpa duplikasi search input.
  4. Memvalidasi kelulusan seluruh 16/16 unit tests (`predictions-page.test.tsx`, `market-card.test.tsx`, `market-filter.test.tsx`) dengan Zero-Comment Policy 100%.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/predictions/page.tsx`
  - `omen/web/tests/predictions-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Props pencarian dan sort diselaraskan langsung melalui `MarketCategoryFilter` untuk memastikan DRY (*Don't Repeat Yourself*).
