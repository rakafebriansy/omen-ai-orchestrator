---
id: TICKET-36
title: Implementasi Smart Contract PredictionMarket.sol
status: Done
priority: High
labels: [SmartContract, Solidity]
---

# Deskripsi
Mengembangkan smart contract inti `PredictionMarket.sol` di `omen/contracts/contracts/PredictionMarket.sol` mewarisi `Ownable` dan `ReentrancyGuard` untuk mengelola pasar prediksi dua arah dan taruhan Native ETH.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Arsitektur Kontrak Solidity
- **Data Structures:**
  - `enum MarketStatus { Active, ResolvedYes, ResolvedNo, Cancelled }`
  - `struct Market { uint256 id; string title; uint256 deadline; uint256 totalYesPool; uint256 totalNoPool; MarketStatus status; bool exists; }`
  - `struct UserBet { uint256 yesAmount; uint256 noAmount; bool claimed; }`
- **Fungsi Inti:**
  1. `createMarket(string title, uint256 deadline) external onlyOwner returns (uint256)`
  2. `placeBet(uint256 marketId, bool side) external payable nonReentrant`
  3. `resolveMarket(uint256 marketId, bool result) external onlyOwner nonReentrant`
  4. `claim(uint256 marketId) external nonReentrant`
  5. `cancelMarket(uint256 marketId) external onlyOwner`

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Fungsi createMarket hanya dapat dieksekusi oleh owner kontrak.
- [x] Fungsi placeBet menerima Native ETH dan memvalidasi block.timestamp < deadline.
- [x] Fungsi claim mentransfer payout proporsional secara aman dan mencegah klaim ganda.
- [x] Fungsi cancelMarket memungkinkan 100% refund bagi seluruh partisipan.
- [x] Kompilasi Solidity berhasil 100% tanpa error atau warning.

## Target Lingkup File (Affected Files)
- `omen/contracts/contracts/PredictionMarket.sol`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan smart contract `PredictionMarket.sol` di `omen/contracts/contracts/` mewarisi OpenZeppelin v5 `Ownable` dan `ReentrancyGuard`.
  2. Mengimplementasikan struktur data `MarketStatus` (`Active`, `ResolvedYes`, `ResolvedNo`, `Cancelled`), struct `Market`, dan struct `UserBet`.
  3. Mengimplementasikan fungsi `createMarket` dengan modifier `onlyOwner` dan validasi judul serta batas waktu deadline masa depan.
  4. Mengimplementasikan fungsi `placeBet` dengan penerimaan Native ETH (`msg.value > 0`), validasi pasar aktif, batas deadline, serta pembaharuan pool YES/NO.
  5. Mengimplementasikan fungsi `resolveMarket` dengan modifier `onlyOwner`, proteksi `nonReentrant`, validasi kelampauan deadline, dan peralihan status outcome.
  6. Mengimplementasikan fungsi `cancelMarket` untuk pembatalan darurat pasar oleh owner.
  7. Mengimplementasikan fungsi `claim` dan `calculatePayout` dengan kalkulasi proporsional pool share pemenang, proteksi pencegahan klaim ganda (`bet.claimed = true`), dukungan 100% refund pada pasar yang dibatalkan, serta low-level transfer ETH aman via Checks-Effects-Interactions pattern.
  8. Menambahkan fungsi view helper `getMarket` dan `getUserBet` untuk mempermudah integrasi dApp dan pengujian.
  9. Menjalankan kompilasi `npx hardhat compile --force` (100% lolos dengan 0 error dan 0 warning).
  10. Menjalankan verifikasi TypeScript `npx tsc --noEmit` di `omen/contracts` dan suite vitest `npm run test` di `omen/web` (127 test lolos).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/contracts/PredictionMarket.sol`
  - `nodes/omen/tickets/TICKET-36-prediction-market-contract-implementation.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan OpenZeppelin Contracts v5.x dengan inisialisasi `Ownable(initialOwner)` pada constructor.
  - Mematuhi Checks-Effects-Interactions pattern: penandaan status `claimed = true` dilakukan sebelum eksekusi transfer ETH via low-level `call{value: payout}("")` guna mengeliminasi potensi reentrancy attack.
