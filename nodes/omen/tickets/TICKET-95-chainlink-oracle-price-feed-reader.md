---
id: TICKET-95
title: Integrasi Chainlink Oracle Price Feed Reader (ETH/USD, BTC/USD, SOL/USD)
status: Done
priority: High
labels: [Oracle, Chainlink, SmartContract, Backend]
---

# Deskripsi
OMEN V1 mengandalkan Chainlink Data Feeds sebagai sumber kebenaran deterministik untuk menyelesaikan pasar keyakinan berbasis metrik harga kripto (misal: "ETH akan melewati $4,000" atau "SOL akan mengungguli performa ETH").

Tiket ini mencakup:
1. Menyusun interface `IChainlinkFeed.sol` (AggregatorV3Interface) pada `omen/contracts/src/interfaces/IChainlinkFeed.sol`.
2. Menyusun modul helper `lib/oracle/chainlink.ts` pada frontend/backend `omen/web` untuk membaca data feed secara on-chain via Viem client.
3. Mendukung kalkulasi 3 model resolusi:
   - `PRICE_ABOVE`: `priceEnd >= targetPrice` -> AGREE_WON, jika tidak DISAGREE_WON.
   - `PRICE_BELOW`: `priceEnd <= targetPrice` -> AGREE_WON, jika tidak DISAGREE_WON.
   - `RELATIVE_PERFORMANCE`: `((priceA_End - priceA_Start) / priceA_Start) > ((priceB_End - priceB_Start) / priceB_Start)` -> AGREE_WON, jika tidak DISAGREE_WON.
4. Menyiapkan alamat feed resmi Ethereum Sepolia untuk pasangan `ETH/USD`, `BTC/USD`, dan `SOL/USD`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menyusun interface `omen/contracts/src/interfaces/IChainlinkFeed.sol`.
- [x] Mengimplementasikan helper `omen/web/lib/oracle/chainlink.ts` dengan method `getLatestPrice(feedAddress)` dan `evaluateResolution(...)`.
- [x] Menangani normalisasi desimal Chainlink (8 desimal untuk harga USD) dengan presisi BigInt.
- [x] Menyediakan penanganan toleransi data usang (*stale price check*) berbasis timestamp `updatedAt`.
- [x] Menyusun unit test pada `omen/web/tests/oracle-chainlink.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/contracts/src/interfaces/IChainlinkFeed.sol`
- `omen/web/lib/oracle/chainlink.ts`
- `omen/web/tests/oracle-chainlink.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/oracle-chainlink.test.ts` untuk normalisasi desimal 8 & 18 Chainlink, kalkulasi resolusi 3 model (`PRICE_ABOVE`, `PRICE_BELOW`, `RELATIVE_PERFORMANCE`), eksekusi on-chain `getLatestPrice` via Viem readContract, dan penanganan stale price threshold.
  2. Mengimplementasikan helper `omen/web/lib/oracle/chainlink.ts` dengan alamat resmi Sepolia Chainlink data feeds (`ETH_USD`, `BTC_USD`, `SOL_USD`), ABI AggregatorV3, normalisasi presisi tinggi BigInt, dan evaluasi hasil deterministik.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/oracle-chainlink.test.ts` -> 6/6 passing 100%) dan ESLint (`npx eslint lib/oracle/chainlink.ts tests/oracle-chainlink.test.ts` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/oracle/chainlink.ts`
  - `omen/web/tests/oracle-chainlink.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengimplementasikan validasi stale price ketat berbasis selisih detik timestamp `updatedAt` on-chain untuk mencegah manipulasi atau keterlambatan pembaruan feed oracle.
