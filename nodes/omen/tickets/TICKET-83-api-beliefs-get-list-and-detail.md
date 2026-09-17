---
id: TICKET-83
title: Pembuatan API Route Beliefs (GET /api/beliefs & GET /api/beliefs/[id])
status: Done
priority: High
labels: [Backend, API, Supabase, Beliefs]
---

# Deskripsi
Tiket ini bertujuan membangun Next.js serverless route handlers untuk menyajikan katalog keyakinan sosial publik serta rincian spesifik satu belief.

Endpoint yang dibangun:
1. `GET /api/beliefs`:
   - Query params: `status` (`DETECTED`, `CONFIRMED`, `CLOSED`, `RESOLVED`, `ALL`), `author`, `sort` (`newest`, `highest_confidence`), `limit`, `offset`.
   - Mengambil data dari tabel `beliefs` dengan relasi ke `belief_sources` dan `markets`.
2. `GET /api/beliefs/[id]`:
   - Mengambil detail belief tunggal berdasarkan UUID dengan join lengkap ke tabel `belief_sources`, `markets`, `creator_confirmations`, dan `creator_profiles`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/app/api/beliefs/route.ts` untuk `GET /api/beliefs`.
- [x] Mengimplementasikan `omen/web/app/api/beliefs/[id]/route.ts` untuk `GET /api/beliefs/[id]`.
- [x] Mendukung filter query parameters, sorting, dan pagination yang efisien.
- [x] Mengembalikan HTTP 404 jika ID belief tidak ditemukan dan HTTP 500 untuk error database.
- [x] Menyusun unit test pada `omen/web/tests/api-beliefs-get.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/route.ts`
- `omen/web/app/api/beliefs/[id]/route.ts`
- `omen/web/tests/api-beliefs-get.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test TDD di `omen/web/tests/api-beliefs-get.test.ts` untuk memverifikasi list pagination, sorting `highest_confidence` / `newest`, filter status dan author, detail query dengan relasi `belief_sources`, `markets`, `creator_confirmations`, error 404 saat data tidak ditemukan, dan error 500 untuk kegagalan database.
  2. Mengimplementasikan serverless handler `GET /api/beliefs` di `omen/web/app/api/beliefs/route.ts` yang mendukung filtering status, case-insensitive author search, limit, offset, dan sorting.
  3. Mengimplementasikan serverless handler `GET /api/beliefs/[id]` di `omen/web/app/api/beliefs/[id]/route.ts` dengan join relasi lengkap dan error handling 404.
  4. Menjalankan Vitest unit testing: seluruh 7 test `api-beliefs-get.test.ts` lulus 100%.
  5. Memvalidasi type checking `tsc --noEmit` dan linter `eslint` dengan 0 error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/beliefs/route.ts` (API route endpoint katalog keyakinan publik)
  - `omen/web/app/api/beliefs/[id]/route.ts` (API route endpoint detail single belief)
  - `omen/web/tests/api-beliefs-get.test.ts` (Unit test suite untuk endpoint GET beliefs)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan query join native Supabase/PostgreSQL untuk menyajikan entitas terkait (`belief_sources`, `markets`, `creator_confirmations`) dalam 1 round-trip query.
  - Zero-Comment Policy ditegakkan 100% pada seluruh berkas kode.
