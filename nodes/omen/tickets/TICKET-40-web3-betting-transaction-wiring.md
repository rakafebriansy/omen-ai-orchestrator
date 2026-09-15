---
id: TICKET-40
title: Integrasi Transaksi Taruhan pada Betting Modal
status: Todo
priority: High
labels: [Frontend, Web3, Integration]
---

# Deskripsi
Menghubungkan tombol konfirmasi pada `BettingModal` ke fungsi `placeBet` smart contract via Wagmi hook `usePlaceBet` dan mencatat transaksi ke `/api/bets/index`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Integrasi Transaksi
- Custom hook `usePlaceBet` memicu `writeContract` memanggil `placeBet(marketId, side)` dengan nilai `value: parseEther(amount)`.
- Menangani siklus hidup transaksi: Pending User Signature -> Broadcasting -> Receipt Confirmed.
- Memicu pemanggilan API `POST /api/bets/index` saat transaksi on-chain terkonfirmasi.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Transaksi placeBet memicu pop-up konfirmasi di Phantom Wallet dengan nominal ETH tepat.
- [ ] Modal menampilkan state loading saat transaksi sedang diproses di blockchain.
- [ ] Pencatatan riwayat taruhan dan poin tersinkronisasi ke database pasca konfirmasi.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/usePlaceBet.ts`
- `omen/web/components/BettingModal.tsx`
- `omen/web/tests/use-place-bet.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
