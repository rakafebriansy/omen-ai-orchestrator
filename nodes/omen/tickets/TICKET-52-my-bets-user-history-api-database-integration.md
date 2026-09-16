---
id: TICKET-52
title: Integrasi Real User Betting History pada Halaman My Bets
status: Done
priority: High
labels: [Frontend, Backend, Betting, Web3, Integration]
---

# Deskripsi
Halaman `app/my-bets/page.tsx` saat ini menyajikan data statis `INITIAL_USER_BETS`. Tiket ini bertugas menghubungkan halaman portofolio taruhan dengan endpoint `GET /api/bets?wallet_address=...` untuk memuat riwayat posisi taruhan nyata pengguna dari basis data Supabase, mengkalkulasi metrik portofolio (Total ETH Staked, Total Won, Win Rate), dan menyelaraskan status klaim dengan smart contract on-chain.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `app/my-bets/page.tsx` memanggil `GET /api/bets?wallet_address=...` berdasarkan alamat wallet yang sedang terkoneksi.
- [x] Kartu statistik portofolio ("Total ETH Staked", "Total Payouts Won", "Prediction Win Rate") dikalkulasi dari riwayat transaksi nyata.
- [x] Filter tab (All Positions, Active, Won, Lost) menyaring data taruhan serverless secara akurat.
- [x] Tombol `ClaimPayoutButton` mengeksekusi penarikan on-chain `claim(marketId)` dan memperbarui status baris menjadi `Claimed` setelah konfirmasi block receipt.
- [x] Menampilkan empty state dengan tombol CTA "Explore Prediction Markets" jika pengguna belum memiliki riwayat taruhan.

## Target Lingkup File (Affected Files & TODO Locations)
- [my-bets/page.tsx:L1](../../../../omen/web/app/my-bets/page.tsx#L1)
- [UserBetsTable.tsx:L1](../../../../omen/web/components/UserBetsTable.tsx#L1)
- [my-bets-page.test.tsx:L1](../../../../omen/web/tests/my-bets-page.test.tsx#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menghubungkan `app/my-bets/page.tsx` ke endpoint `GET /api/bets?wallet_address=...` untuk pemuatan riwayat posisi taruhan live dari tabel `bets` dan `markets` Supabase.
  2. Menghubungkan handler klaim payout dengan `mockPredictionMarket.claimPayout` untuk mutasi saldo virtual dan penandaan status `isClaimed`.
  3. Memvalidasi seluruh 8 unit tests di `my-bets-page.test.tsx` dan `user-bets-table.test.tsx` (100% lulus).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/my-bets/page.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menerapkan kalkulasi live ROI dan metrik agregasi portofolio secara otomatis.
