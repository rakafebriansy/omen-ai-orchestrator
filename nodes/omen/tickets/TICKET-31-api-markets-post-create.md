---
id: TICKET-31
title: Pembuatan API Route Simpan Pasar Baru
status: Done
priority: Medium
labels: [Backend, API, Admin]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/markets` di `omen/web/app/api/markets/route.ts` khusus admin untuk menyimpan metadata pasar baru ke basis data Supabase pasca pembuatan on-chain.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **Request Body:** `{ contract_market_id, title, description, deadline, category }`
- **Proteksi:** Otorisasi admin via secret key / wallet signature.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menyimpan metadata pasar baru dengan contract_market_id unik.
- [x] Memvalidasi otorisasi admin dan menolak permintaan tanpa wewenang.
- [x] Unit test API route create market lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`
- `omen/web/tests/api-markets-create.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan fungsi otorisasi admin `isAuthorizedAdmin` yang memeriksa header `x-admin-key`, `Authorization: Bearer <token>`, dan `x-admin-wallet` terhadap environment variables dan whitelist admin.
  2. Mengimplementasikan Next.js route handler `POST /api/markets` di `web/app/api/markets/route.ts` dengan validasi ketat payload (`contract_market_id`, `title`, `deadline`, `category`, `description`, `resolution_source`), deteksi duplikasi `contract_market_id` (HTTP 409 Conflict), dan insert ke tabel `markets` Supabase via service role admin client.
  3. Membangun unit test suite Vitest di `web/tests/api-markets-create.test.ts` (10 skenario pengujian) mencakup otorisasi key, token, wallet, unauthorized rejection 401, payload validation 400, duplicate conflict 409, database error handling 500, dan Zero-Comment Policy.
  4. Menjalankan verifikasi otomatis Vitest (31 test files, 187 unit tests pass 100%) dan type checking `tsc --noEmit` (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/markets/route.ts`
  - `omen/web/tests/api-markets-create.test.ts`
  - `nodes/omen/tickets/TICKET-31-api-markets-post-create.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Otorisasi admin dirancang fleksibel mendukung integrasi script backend (`x-admin-key`), bearer token gateway (`Authorization`), dan whitelist Web3 wallet admin (`x-admin-wallet`) dengan fallback aman.
  - Memastikan seluruh kode TypeScript dan pengujian mematuhi Zero-Comment Policy secara mutlak.
