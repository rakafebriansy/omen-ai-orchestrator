---
id: TICKET-36
title: Implementasi Smart Contract PredictionMarket.sol
status: Todo
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
- [ ] Fungsi createMarket hanya dapat dieksekusi oleh owner kontrak.
- [ ] Fungsi placeBet menerima Native ETH dan memvalidasi block.timestamp < deadline.
- [ ] Fungsi claim mentransfer payout proporsional secara aman dan mencegah klaim ganda.
- [ ] Fungsi cancelMarket memungkinkan 100% refund bagi seluruh partisipan.
- [ ] Kompilasi Solidity berhasil 100% tanpa error atau warning.

## Target Lingkup File (Affected Files)
- `omen/contracts/contracts/PredictionMarket.sol`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
