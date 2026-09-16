---
id: TICKET-51
title: Integrasi Real Leaderboard & Ranking User pada Halaman Leaderboard
status: Done
priority: Medium
labels: [Frontend, Backend, Leaderboard, Gamification, Integration]
---

# Deskripsi
Halaman `app/leaderboard/page.tsx` saat ini menampilkan data dummy `FULL_LEADERBOARD_DATA` dan mock user address. Tiket ini bertugas menghubungkan halaman leaderboard ke endpoint backend `GET /api/leaderboard/points` dengan dukungan paginasi, pencarian, dan kalkulasi peringkat dinamis wallet pengguna aktif (`currentUserRank`).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `app/leaderboard/page.tsx` memanggil `GET /api/leaderboard/points?limit=50&offset=0` serta menyertakan `wallet_address` dari wallet aktif.
- [x] Kartu ringkasan metrik ("Your Current Rank", "Your Total Points", "Gap to Next Tier") dikalkulasi berdasarkan profil pengguna nyata di Supabase.
- [x] Mendukung pencarian instan berdasarkan address atau ENS name.
- [x] Menangani state loading skeleton dan empty state jika belum ada pengguna yang terdaftar.

## Target Lingkup File (Affected Files & TODO Locations)
- [leaderboard/page.tsx:L1](../../../../omen/web/app/leaderboard/page.tsx#L1)
- [leaderboard-page.test.tsx:L1](../../../../omen/web/tests/leaderboard-page.test.tsx#L1)
- [leaderboard-table.test.tsx:L1](../../../../omen/web/tests/leaderboard-table.test.tsx#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menghubungkan `app/leaderboard/page.tsx` ke endpoint `GET /api/leaderboard/points?limit=50&offset=0` untuk pemuatan ranking live dan currentUserRank.
  2. Mempertahankan filter pencarian instan dan rendering tabel terurut.
  3. Memvalidasi kelulusan 100% pada `leaderboard-page.test.tsx` dan `leaderboard-table.test.tsx`.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/leaderboard/page.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengadopsi headless user rank aggregation untuk memastikan responsivitas halaman tetap instan.
