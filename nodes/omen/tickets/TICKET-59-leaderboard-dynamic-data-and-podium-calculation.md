---
id: TICKET-59
title: Integrasi Dynamic Leaderboard & Kalkulasi Podium Real-time dari Supabase
status: Done
priority: High
labels: [Frontend, Backend, Feature, Supabase, Leaderboard]
---

# Deskripsi
Halaman `app/leaderboard/page.tsx` dan komponen `LeaderboardTable.tsx` masih mengandalkan dataset statis `FULL_LEADERBOARD_DATA` (baris 8–21), konstanta alamat hardcoded `CURRENT_USER`, rank awal `#4`, poin `52300`, serta kalkulasi podium statis (`+29,100 PTS` ke `#3 satoshi-prophet.eth`).

Tiket ini bertujuan untuk menghapus dataset statis `FULL_LEADERBOARD_DATA` dan `DEFAULT_LEADERBOARD_ENTRIES`, mengintegrasikan data ranking secara menyeluruh dari `GET /api/leaderboard/points`, mengkalkulasi podium dan jarak poin ke rank atas secara dinamis berdasarkan data pengguna Supabase, serta menyediakan loading skeleton dan empty state.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menghapus data statis `FULL_LEADERBOARD_DATA` pada `omen/web/app/leaderboard/page.tsx` dan `DEFAULT_LEADERBOARD_ENTRIES` pada `omen/web/components/LeaderboardTable.tsx`.
- [x] Menghapus alamat hardcoded `CURRENT_USER = "0x1234..."` dan menggunakan alamat wallet aktif pengguna.
- [x] Menghubungkan kueri live ranking dengan pagination dan pencarian melalui `GET /api/leaderboard/points?wallet_address=...`.
- [x] Mengkalkulasi posisi rank pengguna saat ini, persentase airdrop tier, dan selisih poin ke peringkat di atasnya secara dinamis dari response API.
- [x] Menyediakan *skeleton loading state* dan penanganan tabel kosong yang bersih.
- [x] Seluruh unit tests Vitest di `omen/web` lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/leaderboard/page.tsx`
- `omen/web/components/LeaderboardTable.tsx`
- `omen/web/tests/leaderboard-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan test suite TDD pada `web/tests/leaderboard-page.test.tsx` untuk memvalidasi fetching dynamic ranking, user profile rank/points, filtering pencarian ENS/address, dan empty state.
  2. Menghapus dataset statis `FULL_LEADERBOARD_DATA` dan konstanta `CURRENT_USER` pada `web/app/leaderboard/page.tsx`.
  3. Menghapus `DEFAULT_LEADERBOARD_ENTRIES` pada `web/components/LeaderboardTable.tsx` dan mengimplementasikan state murni dinamis dengan loading skeleton.
  4. Memvalidasi kelulusan 9/9 unit tests pada `tests/leaderboard-page.test.tsx` dan `tests/leaderboard-table.test.tsx` dengan Zero-Comment Policy 100%.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/leaderboard/page.tsx`
  - `omen/web/components/LeaderboardTable.tsx`
  - `omen/web/tests/leaderboard-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Kalkulasi selisih poin podium (Gap to Next Tier) dihitung langsung terhadap posisi trader rank-3 atau rank tepat di atas pengguna saat ini.
