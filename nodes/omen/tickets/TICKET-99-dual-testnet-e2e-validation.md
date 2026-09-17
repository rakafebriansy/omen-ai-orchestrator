---
id: TICKET-99
title: Validasi Siklus Hidup Penuh End-to-End pada Dual Testnet (Sepolia & Robinhood Chain)
status: Done
priority: High
labels: [Testing, E2E, Web3, MultiChain]
---

# Deskripsi
Tiket ini menyusun dan mengeksekusi rangkaian pengujian End-to-End (E2E) otomatis untuk memvalidasi siklus hidup penuh (*full lifecycle*) protokol OMEN V1 di kedua jaringan (Ethereum Sepolia dan Robinhood Chain Testnet).

Siklus hidup yang diverifikasi:
1. **Penciptaan Belief & Pasar**: Input teks opini -> Ekstraksi AI terstruktur -> Konfirmasi -> Pembuatan kontrak pasar `OmenMarket` via `OmenFactory`.
2. **Penempatan Posisi (Trading)**:
   - Pengguna A: Connect Wallet -> Menyetor posisi `AGREE` dengan ETH.
   - Pengguna B: Connect Wallet -> Menyetor posisi `DISAGREE` dengan ETH.
   - Verifikasi pembaruan pool dan penghitungan rasio konsensus.
3. **Konfirmasi Kreator (EIP-712)**: Kreator melakukan sign typed data -> Status keyakinan berubah menjadi `CONFIRMED`.
4. **Penyelesaian Pasar (Resolution Engine)**: Deadline tercapai -> Pengambilan snapshot harga Chainlink -> Eksekusi fungsi `resolveMarket` on-chain.
5. **Klaim Kemenangan (Settlement)**: Pengguna pemenang memanggil `claimPayout()` -> Penambahan saldo ETH berhasil terverifikasi.
6. **Verifikasi Kasus Batal (VOID)**: Skenario kegagalan data oracle menghasilkan penarikan refund penuh 100%.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menyusun test suite E2E komprehensif pada `omen/web/tests/e2e/belief-market-cycle.test.tsx`.
- [x] Memvalidasi seluruh transisi state dari `OPEN`, `CLOSED`, `RESOLVED`, hingga `SETTLED` dan `VOID`.
- [x] Memvalidasi kalkulasi payout proporsional dan proteksi pencegahan klaim ganda.
- [x] Memastikan seluruh rangkaian test berjalan mulus dan lulus 100% pada lingkungan Vitest.
- [x] Mematuhi Zero-Comment Policy pada seluruh file pengujian.

## Target Lingkup File (Affected Files)
- `omen/web/tests/e2e/belief-market-cycle.test.tsx`
- `omen/web/tests/e2e/dual-chain-workflow.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan suite pengujian E2E `tests/e2e/belief-market-cycle.test.tsx` yang memvalidasi siklus hidup penuh (deploy via `useCreateMarket`, stake AGREE via `usePosition`, autentikasi EIP-712 via `useCreatorConfirm`, kalkulasi Chainlink oracle deterministik, dan penyelesaian payout via `useClaim`).
  2. Mengembangkan suite pengujian dual-chain `tests/e2e/dual-chain-workflow.test.ts` memverifikasi konfigurasi dual testnet (Ethereum Sepolia `11155111` dan Robinhood Chain Testnet `46630`), kalkulasi payout proporsional, dan penanganan refund pasar VOID.
  3. Memvalidasi 6/6 test lulus 100% pada Vitest dan ESLint dengan kepatuhan penuh Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `web/lib/wagmi.ts`
  - `web/lib/oracle/chainlink.ts`
  - `web/hooks/usePosition.ts`
  - `web/tests/e2e/belief-market-cycle.test.tsx`
  - `web/tests/e2e/dual-chain-workflow.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengintegrasikan fungsi utilitas `calculateResolutionResult` pada `lib/oracle/chainlink.ts` untuk pemetaan hasil resolusi pasar deterministik.
