---
id: TICKET-47
title: Implementasi Mock Contract Engine & Web3 Simulator Provider
status: Done
priority: High
labels: [Frontend, Web3, MockEngine, Simulator, Architecture]
---

# Deskripsi
Untuk memungkinkan pengembangan, pengujian, dan validasi seluruh fitur platform Omen secara mulus tanpa ketergantungan pada ekstensi dompet browser, gas fee, atau jaringan testnet eksternal, tiket ini bertugas membangun **Mock Contract & Web3 Simulator Engine** (`lib/mockPredictionMarket.ts`).

Engine simulator ini menyediakan emulasi lengkap state blockchain lokal, pembuatan hash transaksi realistis, manajemen saldo ETH virtual, serta hook pemanggilan fungsi pasar prediksi (`placeBet`, `claimPayout`, `createMarket`, `resolveMarket`, `cancelMarket`) yang dapat diaktifkan melalui flag `NEXT_PUBLIC_USE_MOCK_CONTRACT="true"`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Membuat modul simulator `omen/web/lib/mockPredictionMarket.ts` yang mengemulasi seluruh interface `PredictionMarket.sol`.
- [x] Menyediakan akun demo bawaan (`NEXT_PUBLIC_DEMO_WALLET_ADDRESS` / `0x71C...B29`) dengan saldo awal 10.0 ETH virtual.
- [x] Fungsi `placeBet` mensimulasikan hash transaksi instan, memvalidasi kuota odds, memperbarui pool YES/NO in-memory, dan memancarkan callback event untuk sinkronisasi database.
- [x] Fungsi `claimPayout`, `createMarket`, `resolveMarket`, dan `cancelMarket` berfungsi secara reaktif dengan delay asinkron realistis (~300ms).
- [x] Menyediakan pengujian otomatis `omen/web/tests/mock-prediction-market.test.ts` dengan kelulusan 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- [mockPredictionMarket.ts:L1](../../../../omen/web/lib/mockPredictionMarket.ts#L1)
- [contracts.ts:L1](../../../../omen/web/lib/contracts.ts#L1)
- `omen/web/.env.local`
- [mock-prediction-market.test.ts:L1](../../../../omen/web/tests/mock-prediction-market.test.ts#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun modul simulator in-memory singleton `MockPredictionMarketEngine` di `web/lib/mockPredictionMarket.ts` yang mengemulasi pool likuiditas dinamis, deterministic fake txHash generator, dan mutasi saldo ETH virtual (10.0 ETH).
  2. Mengekspor flag `USE_MOCK_CONTRACT` di `web/lib/contracts.ts` untuk transisi transparan antar mock dan live Web3 mode.
  3. Menyusun unit test suite Vitest di `web/tests/mock-prediction-market.test.ts` mencakup 8 skenario (inits, balance checks, placing YES/NO bets, invalid amounts, market creation, resolution, cancellation, dan claim payout).
  4. Seluruh 29 test files (158 tests) di `web` lulus 100% dan mematuhi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/mockPredictionMarket.ts`, `omen/web/lib/contracts.ts`, `omen/web/tests/mock-prediction-market.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan arsitektur adapter terisolasi sehingga transisi ke smart contract nyata di Arbitrum Sepolia hanya membutuhkan toggle satu environment variable.
