---
id: TICKET-86
title: Refactor API Route Markets V1 (GET /api/markets & GET /api/markets/[id])
status: Done
priority: High
labels: [Backend, API, Markets, Supabase]
---

# Deskripsi
Endpoint pasar yang sudah ada (`GET /api/markets`) perlu diselaraskan dengan skema V1 dan model Social Belief.

Perubahan yang dilakukan:
1. `GET /api/markets`:
   - Melakukan relasi (*join*) tabel `markets` dengan `beliefs`, `belief_sources`, dan `creator_profiles`.
   - Mengkalkulasi metrik dinamis:
     - `opinion_consensus`: persentase partisipan `agree_count / (agree_count + disagree_count)`.
     - `capital_consensus`: persentase dana `agree_pool / (agree_pool + disagree_pool)`.
   - Mendukung filter tab: `trending` (kombinasi volume & partisipan), `newest`, `ending_soon`, `most_volume`, `confirmed`.
   - Mendukung pencarian berbasis teks keyakinan atau author handle.
2. `GET /api/markets/[id]`:
   - Mengambil detail lengkap satu pasar berdasarkan UUID atau `contract_address`, mencakup snapshot oracle, riwayat event, dan status resolusi.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memperbarui `omen/web/app/api/markets/route.ts` untuk mendukung skema V1 dan filter tab discovery.
- [x] Mengimplementasikan `omen/web/app/api/markets/[id]/route.ts` untuk detail lengkap pasar.
- [x] Menghitung rasio konsensus opini dan rasio pool kapital secara akurat dan aman terhadap pembagian dengan nol.
- [x] Mengembalikan relasi data belief dan profil kreator dalam bentuk JSON terstruktur.
- [x] Menyusun unit test pada `omen/web/tests/api-markets-v1-get.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`
- `omen/web/app/api/markets/[id]/route.ts`
- `omen/web/tests/api-markets-v1-get.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test TDD di `omen/web/tests/api-markets-v1-get.test.ts` untuk menguji penghitungan `capital_consensus`, penyertaan relasi `beliefs`, filter tab discovery (`trending`, `newest`, `ending_soon`, `most_volume`, `confirmed`), serta detail query pasar via UUID dan contract address dengan penanganan 404 & 500.
  2. Memperbarui `omen/web/app/api/markets/route.ts` untuk mendukung skema V1 (menghitung `capital_consensus` dan `total_pool`, join `beliefs` & `belief_sources`) sambil menjaga kompatibilitas mundur (backward-compatibility) dengan kontrak API V0.
  3. Mengimplementasikan `omen/web/app/api/markets/[id]/route.ts` untuk query detail pasar komprehensif berdasarkan UUID atau `contract_address` dengan relasi ke `oracle_snapshots`, `market_resolutions`, `market_positions`, dan `beliefs`.
  4. Menjalankan pengujian Vitest: seluruh 6 test `api-markets-v1-get.test.ts` dan 277 total test aplikasi lulus 100%.
  5. Memvalidasi type checking `tsc --noEmit` dan linter `eslint` dengan 0 error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/markets/route.ts` (Endpoint katalog pasar terintegrasi V1)
  - `omen/web/app/api/markets/[id]/route.ts` (Endpoint detail tunggal pasar V1)
  - `omen/web/tests/api-markets-v1-get.test.ts` (Unit test suite untuk API markets V1)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Kalkulasi `capital_consensus` diproteksi secara matematis terhadap division by zero (default 50% jika pool masih kosong).
  - Skema join database efisien dan mematuhi Zero-Comment Policy secara ketat.
