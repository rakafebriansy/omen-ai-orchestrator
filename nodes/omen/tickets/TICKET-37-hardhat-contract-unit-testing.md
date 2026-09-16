---
id: TICKET-37
title: Unit Testing Hardhat PredictionMarket.sol
status: Done
priority: High
labels: [SmartContract, Testing]
---

# Deskripsi
Membangun rangkaian pengujian unit test Hardhat komprehensif di `omen/contracts/test/PredictionMarket.test.ts` untuk memverifikasi matematika odds, distribusi pool, keamanan reentrancy, dan penanganan kasus batas.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Skenario Test Suite
1. Pembuatan pasar sukses dan penolakan jika dipanggil non-owner.
2. Pemasangan taruhan Yes dan No dengan nominal ETH yang sesuai.
3. Penolakan taruhan jika batas deadline telah lewat.
4. Resolusi pasar Yes dan klaim payout proporsional bagi pemenang Yes.
5. Resolusi pasar No dan klaim payout proporsional bagi pemenang No.
6. Pencegahan klaim ganda oleh akun yang sama.
7. Pembatalan pasar (cancelMarket) dan penarikan refund 100%.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Seluruh skenario unit test lulus 100% tanpa kegagalan.
- [x] Pengujian mencakup proteksi akses unauthorized non-owner.
- [x] Pengujian memvalidasi keakuratan saldo transfer payout Native ETH.

## Target Lingkup File (Affected Files)
- `omen/contracts/test/PredictionMarket.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat test suite Hardhat `omen/contracts/test/PredictionMarket.test.ts` berbasis TypeScript, Mocha/Chai, dan ethers v6.
  2. Menyusun 19 skenario pengujian komprehensif terbagi dalam 7 grup pengujian:
     - `Market Creation`: Validasi inisialisasi pasar oleh owner, pencegahan akses unauthorized non-owner (`OwnableUnauthorizedAccount`), validasi judul non-kosong, dan validasi batas deadline di masa depan.
     - `Betting Lifecycle`: Validasi taruhan kubu YES/NO dalam Native ETH, emisi event `BetPlaced`, pencegahan taruhan 0 ETH, pasar tidak eksis, dan penolakan taruhan saat deadline kadaluarsa.
     - `Market Resolution`: Validasi resolusi outcome YES/NO setelah deadline, proteksi akses non-owner, pencegahan resolusi prematur, dan pencegahan resolusi ganda.
     - `Proportional Payout Claims (YES Winner)`: Kalkulasi matematika pool share multi-bettor, verifikasi pertambahan saldo Native ETH dengan `changeEtherBalance`, penolakan klaim kubu kalah, dan pencegahan klaim ganda (`Payout already claimed`).
     - `Proportional Payout Claims (NO Winner)`: Kalkulasi proporsional saat kubu NO menang dan verifikasi transfer payout.
     - `Market Cancellation & 100% Refunds`: Pembatalan pasar darurat oleh owner, emisi `MarketCancelled`, dan penarikan refund 100% bagi seluruh partisipan.
     - `Edge Cases & State Checks`: Validasi pengembalian modal pada pool satu sisi (one-sided bet), penolakan klaim pada pasar aktif, dan penolakan query pasar tidak eksis.
  3. Menjalankan eksekusi `npx hardhat test` dengan hasil 19 passing (100% lulus).
  4. Menjalankan validasi TypeScript `npx tsc --noEmit` (lolos tanpa error).
  5. Menjalankan suite pengujian web `npm run test` di `omen/web` (127 test lolos).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/test/PredictionMarket.test.ts`
  - `nodes/omen/tickets/TICKET-37-hardhat-contract-unit-testing.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan fixture pattern `loadFixture(deployPredictionMarketFixture)` untuk isolasi mutlak antar pengujian tanpa polusi state.
  - Memanfaatkan network helper `time.increaseTo` untuk pengujian manipulasi waktu blok secara deterministik.
