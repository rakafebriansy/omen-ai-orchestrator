---
id: TICKET-95
title: Integrasi Chainlink Oracle Price Feed Reader (ETH/USD, BTC/USD, SOL/USD)
status: Todo
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
- [ ] Menyusun interface `omen/contracts/src/interfaces/IChainlinkFeed.sol`.
- [ ] Mengimplementasikan helper `omen/web/lib/oracle/chainlink.ts` dengan method `getLatestPrice(feedAddress)` dan `evaluateResolution(...)`.
- [ ] Menangani normalisasi desimal Chainlink (8 desimal untuk harga USD) dengan presisi BigInt.
- [ ] Menyediakan penanganan toleransi data usang (*stale price check*) berbasis timestamp `updatedAt`.
- [ ] Menyusun unit test pada `omen/web/tests/oracle-chainlink.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/contracts/src/interfaces/IChainlinkFeed.sol`
- `omen/web/lib/oracle/chainlink.ts`
- `omen/web/tests/oracle-chainlink.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
