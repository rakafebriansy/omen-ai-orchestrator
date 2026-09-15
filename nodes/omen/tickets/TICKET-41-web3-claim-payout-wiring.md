---
id: TICKET-41
title: Integrasi Transaksi Klaim pada Halaman My Bets
status: Todo
priority: High
labels: [Frontend, Web3, Integration]
---

# Deskripsi
Menghubungkan tombol `ClaimPayoutButton` ke fungsi `claim` smart contract via Wagmi hook `useClaimPayout` untuk mentransfer dana kemenangan ETH ke dompet pengguna.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Integrasi Klaim
- Custom hook `useClaimPayout` memanggil fungsi `claim(marketId)` pada kontrak.
- Memperbarui status tombol menjadi 'Claimed' setelah transaksi penarikan berhasil terkonfirmasi.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memicu transaksi on-chain claim(marketId) ke smart contract.
- [ ] Dana kemenangan ETH berhasil masuk ke saldo dompet pemenang.
- [ ] Status tombol terbarui secara reaktif.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useClaimPayout.ts`
- `omen/web/components/ClaimPayoutButton.tsx`
- `omen/web/tests/use-claim-payout.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
