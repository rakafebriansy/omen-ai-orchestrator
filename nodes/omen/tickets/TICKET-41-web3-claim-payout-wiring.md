---
id: TICKET-41
title: Integrasi Transaksi Klaim pada Halaman My Bets
status: Todo
priority: High
labels: [Frontend, Web3, Integration]
---

# Deskripsi
Menghubungkan tombol ClaimPayoutButton ke fungsi claim di smart contract via Wagmi useWriteContract untuk penarikan dana kemenangan.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memicu transaksi on-chain claim(marketId) ke kontrak.
- [ ] Dana kemenangan ETH tertransfer masuk ke wallet pengguna.
- [ ] Status tombol berubah menjadi 'Sudah Diklaim' setelah transaksi sukses.

## Target Lingkup File (Affected Files)
- `omen/web/components/ClaimPayoutButton.tsx`
- `omen/web/hooks/useClaimPayout.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
