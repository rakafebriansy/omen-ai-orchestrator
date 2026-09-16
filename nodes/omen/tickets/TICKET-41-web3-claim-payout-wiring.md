---
id: TICKET-41
title: Integrasi Transaksi Klaim pada Halaman My Bets
status: Done
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
- [x] Memicu transaksi on-chain claim(marketId) ke smart contract.
- [x] Dana kemenangan ETH berhasil masuk ke saldo dompet pemenang.
- [x] Status tombol terbarui secara reaktif.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useClaimPayout.ts`
- `omen/web/components/ClaimPayoutButton.tsx`
- `omen/web/tests/use-claim-payout.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan custom hook `useClaimPayout` di `omen/web/hooks/useClaimPayout.ts` memanfaatkan `useWriteContract`, `useWaitForTransactionReceipt`, `useAccount`, dan `WagmiContext` dari Wagmi v2.
  2. Menghubungkan fungsi on-chain `claim(marketId)` dengan konversi tipe `BigInt(marketId)` dan parameter smart contract `PredictionMarket`.
  3. Memodifikasi `ClaimPayoutButton.tsx` untuk mendukung prop `marketId` dan `onSuccess`, mengintegrasikan `useClaimPayout`, serta memperbarui status badge menjadi "Claimed" secara reaktif setelah receipt transaksi terkonfirmasi di blockchain.
  4. Menulis unit test suite di `omen/web/tests/use-claim-payout.test.ts` dan memperluas pengujian di `omen/web/tests/claim-button.test.tsx` (5/5 tests pass).
  5. Memvalidasi seluruh test suite (25 test files / 137 tests di `omen/web` lulus 100%, 19 unit tests di `omen/contracts` lulus 100%) dan `tsc --noEmit` 0 galat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/hooks/useClaimPayout.ts`
  - `omen/web/components/ClaimPayoutButton.tsx`
  - `omen/web/tests/use-claim-payout.test.ts`
  - `omen/web/tests/claim-button.test.tsx`
  - `nodes/omen/tickets/TICKET-41-web3-claim-payout-wiring.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengimplementasikan isolasi safe fallback ketika komponen atau hook dirender di luar `WagmiProvider` agar seluruh unit test suite UI terisolasi tetap stabil.
  - Memastikan seluruh kode TypeScript mematuhi aturan Zero-Comment Policy secara mutlak.
