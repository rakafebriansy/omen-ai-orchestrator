---
id: TICKET-29
title: Pembuatan API Route Ranking Poin
status: Done
priority: Medium
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `GET /api/leaderboard/points` di `omen/web/app/api/leaderboard/points/route.ts` untuk menyajikan peringkat global berdasarkan akumulasi total poin.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `GET`
- **Query Params:** `limit` (default 50), `offset` (default 0), `wallet_address` (opsional)
- **Response:** Array ranking pengguna dan objek `currentUserRank`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengurutkan daftar ranking secara descending berdasarkan total_points.
- [x] Mendukung paginasi data limit dan offset.
- [x] Unit test API route leaderboard lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/leaderboard/points/route.ts`
- `omen/web/tests/api-leaderboard.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan serverless Next.js API route handler `GET /api/leaderboard/points` di `omen/web/app/api/leaderboard/points/route.ts`.
  2. Mengimplementasikan paginasi kueri fleksibel dengan query parameters `limit` (default 50, batas aman 1-100) dan `offset` (default 0) menggunakan `.range(offset, offset + limit - 1)` pada PostgreSQL Supabase.
  3. Mengurutkan ranking secara descending berdasarkan `total_points` (dengan tie-breaker `created_at ASC`), serta menghitung posisi absolut `currentUserRank` real-time apabila parameter `wallet_address` disertakan.
  4. Menulis unit test komprehensif di `omen/web/tests/api-leaderboard.test.ts` (5 skenario uji: paginasi default, custom offset/limit, kalkulasi currentUserRank, error handling database 500, dan Zero-Comment Policy).
  5. Memvalidasi seluruh test suite Vitest `npm run test` (29 file, 172 test lolos 100%) dan type check `npx tsc --noEmit` lolos tanpa error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/leaderboard/points/route.ts` (Created)
  - `omen/web/tests/api-leaderboard.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-29-api-points-leaderboard.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan kueri `select('*', { count: 'exact', head: true }).gt('total_points', userPoints)` untuk menghitung rank user saat ini secara efisien tanpa perlu memuat seluruh baris tabel ke memory server.
