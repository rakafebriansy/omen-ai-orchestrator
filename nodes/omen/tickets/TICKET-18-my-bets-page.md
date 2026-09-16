---
id: TICKET-18
title: Pembuatan Halaman My Bets
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman penuh My Bets di `omen/web/app/my-bets/page.tsx` yang memadukan ringkasan portofolio taruhan pribadi pengguna dan daftar tabel riwayat taruhan `UserBetsTable`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Halaman (`app/my-bets/page.tsx`)
1. **Header Halaman:**
   - Judul H1: "My Predictions & Bets" (`text-3xl sm:text-4xl font-extrabold text-zinc-900 dark:text-zinc-100 tracking-tight`).
   - Subjudul ringkas, kicker badge testnet, dan panduan klaim dana hasil prediksi.
2. **Portofolio Summary Cards (3 Kartu):**
   - `grid grid-cols-1 sm:grid-cols-3 gap-5`.
   - Kartu 1: "Total ETH Staked" (contoh: "1.20 ETH").
   - Kartu 2: "Total Payouts Won" (contoh: "1.16 ETH").
   - Kartu 3: "Prediction Win Rate" (contoh: "66.7%").
3. **Tabel Riwayat Taruhan:**
   - Integrasi komponen `UserBetsTable`, kontrol tab filter posisi (*All Positions, Active, Won, Lost*), dan pembaruan klaim payout `ClaimPayoutButton`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Halaman merender 3 kartu statistik portofolio dan tabel riwayat taruhan.
- [x] Menampilkan empty state ramah jika pengguna belum pernah bertaruh.
- [x] Unit test halaman my-bets berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/my-bets/page.tsx`
- `omen/web/tests/my-bets-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun halaman `app/my-bets/page.tsx` yang memadukan 3 kartu metrik portofolio (Total ETH Staked, Total Payouts Won, Prediction Win Rate), tab filter status posisi (All, Active, Won, Lost), serta integrasi tabel riwayat taruhan `<UserBetsTable />` dengan handling klaim payout dinamis dan notifikasi toast konfirmasi sukses.
  2. Menyusun test suite unit testing Vitest `my-bets-page.test.tsx` dengan 3 skenario pengujian komprehensif menguji rendering header & 3 kartu metrik portofolio, penyaringan tab posisi taruhan, dan eksekusi tombol klaim payout yang memperbarui state ke Claimed serta memunculkan status alert feedback.
  3. Memverifikasi seluruh test suite Vitest (total 90/90 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/my-bets/page.tsx` [Created]
  - `omen/web/tests/my-bets-page.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-18-my-bets-page.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan kalkulasi metrik agregasi `useMemo` (Total Staked, Total Won, Win Rate) yang secara otomatis diperbarui ketika terdapat status klaim baru atau penambahan taruhan di portofolio pengguna.
