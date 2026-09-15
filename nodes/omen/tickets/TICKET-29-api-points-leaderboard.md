---
id: TICKET-29
title: Pembuatan API Route Ranking Poin
status: Todo
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
- [ ] Mengurutkan daftar ranking secara descending berdasarkan total_points.
- [ ] Mendukung paginasi data limit dan offset.
- [ ] Unit test API route leaderboard lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/leaderboard/points/route.ts`
- `omen/web/tests/api-leaderboard.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
