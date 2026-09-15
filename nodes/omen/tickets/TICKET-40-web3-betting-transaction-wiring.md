---
id: TICKET-40
title: Integrasi Transaksi Taruhan pada Betting Modal
status: Todo
priority: High
labels: [Frontend, Web3, Integration]
---

# Deskripsi
Menghubungkan tombol konfirmasi pada BettingModal ke fungsi placeBet di smart contract via Wagmi useWriteContract dan mencatat ke API indexer.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memicu popup konfirmasi transaksi di Phantom Wallet dengan nominal ETH yang sesuai.
- [ ] Menampilkan modal status loading hingga transaksi terkonfirmasi di blockchain.
- [ ] Memanggil POST /api/bets/index setelah transaksi berhasil dikonfirmasi.

## Target Lingkup File (Affected Files)
- `omen/web/components/BettingModal.tsx`
- `omen/web/hooks/usePlaceBet.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
