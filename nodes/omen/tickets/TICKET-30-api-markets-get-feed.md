---
id: TICKET-30
title: Pembuatan API Route Katalog Pasar
status: Done
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `GET /api/markets` di `omen/web/app/api/markets/route.ts` untuk menyajikan katalog pasar prediksi dengan filter status dan kategori.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `GET`
- **Query Params:** `status` (active, resolved, all), `category` (crypto, meme, all), `sort` (highest_pool, newest)
- **Response:** Array data pasar prediksi beserta rincian pool Yes dan No.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mendukung filter status pasar dan kategori secara dinamis.
- [x] Mengembalikan kalkulasi total pool dan batas waktu deadline.
- [x] Unit test API route get markets lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`
- `omen/web/tests/api-markets-get.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menambahkan kolom `category` dan indeks `idx_markets_category` pada skema Supabase `web/db/migrations/01_init_schema.sql` dan tipe `web/types/database.ts`.
  2. Membangun Next.js route handler `GET /api/markets` di `web/app/api/markets/route.ts` dengan filter status (`active`, `resolved`, `cancelled`, `all`), filter kategori (`crypto`, `meme`, dll), sorting (`highest_pool`, `ending_soon`, `newest`), dan agregasi kalkulasi `total_pool = yesPool + noPool`.
  3. Membangun test suite Vitest komprehensif di `web/tests/api-markets-get.test.ts` (6 skenario pengujian) mencakup filtering, sorting, agregasi pool, error handling, dan Zero-Comment Policy.
  4. Menjalankan verifikasi pengujian otomatis Vitest (30 test files, 178 unit tests pass 100%) dan type checking `tsc --noEmit` (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/markets/route.ts`
  - `omen/web/tests/api-markets-get.test.ts`
  - `omen/web/db/migrations/01_init_schema.sql`
  - `omen/web/types/database.ts`
  - `omen/web/tests/api-schema.test.ts`
  - `nodes/omen/tickets/TICKET-30-api-markets-get-feed.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan query modifier PostgREST dinamis (`eq`, `in`, `ilike`, `order`) berbasis query parameter untuk performa tinggi tanpa over-fetching.
  - Memastikan seluruh kode TypeScript, SQL, dan test mematuhi Zero-Comment Policy secara mutlak.
