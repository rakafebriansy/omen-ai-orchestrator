---
id: TICKET-40
title: Integrasi Transaksi Taruhan pada Betting Modal
status: Done
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
- [x] Transaksi placeBet memicu pop-up konfirmasi di Phantom Wallet dengan nominal ETH tepat.
- [x] Modal menampilkan state loading saat transaksi sedang diproses di blockchain.
- [x] Pencatatan riwayat taruhan dan poin tersinkronisasi ke database pasca konfirmasi.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/usePlaceBet.ts`
- `omen/web/components/BettingModal.tsx`
- `omen/web/tests/use-place-bet.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan custom hook `usePlaceBet` di `omen/web/hooks/usePlaceBet.ts` memanfaatkan `useWriteContract`, `useWaitForTransactionReceipt`, dan `useAccount` dari Wagmi v2 serta `parseEther` dari Viem.
  2. Mengimplementasikan integrasi transaksi `placeBet(marketId, side)` dengan parameter contract address dan ABI `PredictionMarket`, serta sinkronisasi pasca-konfirmasi ke `POST /api/bets/index`.
  3. Mengintegrasikan `usePlaceBet` ke dalam `omen/web/components/BettingModal.tsx` dengan preservasi backward compatibility untuk prop `onConfirmBet` opsional dan visual loading state pada tombol konfirmasi taruhan.
  4. Menulis unit test suite di `omen/web/tests/use-place-bet.test.ts` mencakup verifikasi parameter pemanggilan fungsi kontrak, konversi wei, penanganan penolakan wallet, dan pemanggilan indexer.
  5. Memvalidasi seluruh test suite (24 test files / 133 tests di `omen/web` lulus 100%, 19 unit tests di `omen/contracts` lulus 100%) dan `tsc --noEmit` 0 galat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/hooks/usePlaceBet.ts`
  - `omen/web/components/BettingModal.tsx`
  - `omen/web/tests/use-place-bet.test.ts`
  - `nodes/omen/tickets/TICKET-40-web3-betting-transaction-wiring.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengimplementasikan pengecekan `WagmiContext` di dalam `usePlaceBet` untuk mengembalikan safe fallback ketika komponen dirender di luar `WagmiProvider` pada unit test suite UI terisolasi.
  - Memastikan seluruh kode TypeScript mematuhi aturan Zero-Comment Policy secara mutlak.
