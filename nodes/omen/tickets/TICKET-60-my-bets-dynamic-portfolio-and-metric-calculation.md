---
id: TICKET-60
title: Integrasi Dynamic Portfolio My Bets & Kalkulasi Metrik Portofolio Real-time
status: Done
priority: High
labels: [Frontend, Backend, Feature, Supabase, Betting]
---

# Deskripsi
Halaman `app/my-bets/page.tsx` masih memiliki data statis `INITIAL_USER_BETS` (baris 7–58) yang menjadi fallback jika data dari API kosong, serta metrik statis net return `+104% Net Return` (baris 176). Selain itu, halaman masih menggunakan demo wallet fallback daripada alamat wallet aktif.

Tiket ini bertujuan untuk menghapus `INITIAL_USER_BETS`, mengintegrasikan data riwayat taruhan murni secara dinamis dari `GET /api/bets?wallet_address=...`, mengkalkulasi metrik total ETH staked, total won, win rate, dan net return secara dinamis dari data transaksi nyata di Supabase, serta memastikan state klaim hadiah terhubung mulus.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menghapus data statis `INITIAL_USER_BETS` pada `omen/web/app/my-bets/page.tsx`.
- [x] Menghapus hardcoded string `+104% Net Return` dan menggantinya dengan kalkulasi persentase ROI/Net Return dinamis dari posisi taruhan nyata.
- [x] Mengambil riwayat taruhan dari `GET /api/bets?wallet_address=...` berdasarkan wallet aktif pengguna dan merender status real (`active`, `won`, `lost`).
- [x] Menampilkan komponen `No Bet Positions Yet` (empty state) secara tepat jika pengguna belum memiliki catatan taruhan (tanpa fallback data statis).
- [x] Menghubungkan tombol klaim kemenangan (`handleClaimPayout`) dengan eksekusi on-chain / mock contract dan pembaruan status live ke Supabase.
- [x] Seluruh unit tests Vitest di `omen/web` lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/my-bets/page.tsx`
- `omen/web/components/UserBetsTable.tsx`
- `omen/web/tests/my-bets-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan test suite TDD pada `web/tests/my-bets-page.test.tsx` untuk memvalidasi fetching riwayat taruhan live, kalkulasi dinamis total ETH staked, total won, win rate %, net return %, klaim payout, dan rendering empty state.
  2. Menghapus dataset statis `INITIAL_USER_BETS` dan string hardcoded `+104% Net Return` dari `web/app/my-bets/page.tsx`.
  3. Mengintegrasikan kalkulasi metrik portofolio dinamis dari data nyata yang ditarik dari `GET /api/bets?wallet_address=...`.
  4. Memvalidasi kelulusan seluruh 10/10 unit tests pada `tests/my-bets-page.test.tsx` dan `tests/user-bets-table.test.tsx` dengan Zero-Comment Policy 100%.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/my-bets/page.tsx`
  - `omen/web/tests/my-bets-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Net return % dikalkulasi dinamis dengan rumus `((totalWon - totalStaked) / totalStaked) * 100` dengan format tanda `+/-`.
