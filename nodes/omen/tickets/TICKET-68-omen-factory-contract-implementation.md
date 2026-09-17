---
id: TICKET-68
title: Implementasi Smart Contract OmenFactory.sol
status: Done
priority: High
labels: [SmartContract, Foundry, Solidity, Factory]
---

# Deskripsi
`OmenFactory.sol` adalah kontrak *factory & registry* utama yang bertugas membuat dan melacak seluruh instans pasar prediksi keyakinan (`OmenMarket`). Kontrak ini menerapkan pemisahan peran (Role-Based Access Control) menggunakan OpenZeppelin `AccessControl` atau `Ownable2Step`.

Sesuai spesifikasi arsitektur V1:
- Teks belief mentah **TIDAK** disimpan on-chain untuk menghemat gas, melainkan hanya hash integritas (`bytes32 beliefHash`, `bytes32 sourceHash`, `bytes32 resolutionHash`).
- Fungsi `createMarket(...)` mendeploy instans `OmenMarket` baru, mencatat alamatnya pada registry internal `mapping(uint256 => address) public markets`, dan memancarkan event `MarketCreated`.
- Mendukung pemisahan role `DEFAULT_ADMIN_ROLE`, `MARKET_CREATOR_ROLE`, dan `RESOLVER_ROLE`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `OmenFactory.sol` di `omen/contracts/src/OmenFactory.sol`.
- [x] Menyediakan fungsi `createMarket(bytes32 beliefHash, bytes32 sourceHash, bytes32 resolutionHash, uint256 openTime, uint256 closeTime, ResolutionConfig calldata config) external returns (address marketAddress)`.
- [x] Mengimplementasikan role-based access control dengan OpenZeppelin AccessControl.
- [x] Menyediakan event `MarketCreated(uint256 indexed marketId, address indexed marketAddress, bytes32 indexed beliefHash, uint256 closeTime)`.
- [x] Menyediakan getter helpers: `getMarket(uint256 marketId)`, `totalMarkets()`, `isMarketValid(address marketAddress)`.
- [x] Mematuhi Zero-Comment Policy dan lulus kompilasi `forge build` 100%.

## Target Lingkup File (Affected Files)
- `omen/contracts/src/OmenFactory.sol`
- `omen/contracts/src/interfaces/IOmenFactory.sol`
- `omen/contracts/src/interfaces/IOmenMarket.sol`
- `omen/contracts/src/types/MarketTypes.sol`
- `omen/contracts/src/OmenMarket.sol`
- `omen/contracts/test/OmenFactory.t.sol`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis test suite TDD Foundry di `omen/contracts/test/OmenFactory.t.sol` untuk memvalidasi inisialisasi role, otorisasi caller `MARKET_CREATOR_ROLE`, validasi rentang waktu (`closeTime > openTime`), penolakan `bytes32(0)` belief hash, registrasi registry `getMarket(id)` & `isMarketValid(addr)`, dan emisi event `MarketCreated`.
  2. Menyusun struktur tipe data pasar di `omen/contracts/src/types/MarketTypes.sol` (`MarketStatus`, `Outcome`, `ResolutionType`, `ResolutionConfig`).
  3. Mendefinisikan antarmuka kontrak `IOmenFactory.sol` dan `IOmenMarket.sol`.
  4. Mengimplementasikan kontrak `OmenMarket.sol` sebagai target instans pasar yang dideploy oleh factory.
  5. Mengimplementasikan kontrak `OmenFactory.sol` dengan role management OpenZeppelin `AccessControl` (`DEFAULT_ADMIN_ROLE`, `MARKET_CREATOR_ROLE`, `RESOLVER_ROLE`) dan fungsi deploy `createMarket`.
  6. Menjalankan `forge test --match-contract OmenFactoryTest -vv` dengan hasil 100% PASS (6 passed, 0 failed).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/src/types/MarketTypes.sol` (Tipe data, enum, dan konfigurasi resolusi V1)
  - `omen/contracts/src/interfaces/IOmenFactory.sol` (Antarmuka publik OmenFactory)
  - `omen/contracts/src/interfaces/IOmenMarket.sol` (Antarmuka publik OmenMarket)
  - `omen/contracts/src/OmenMarket.sol` (Kontrak individual escrow & settlement pasar)
  - `omen/contracts/src/OmenFactory.sol` (Kontrak factory & registry pasar)
  - `omen/contracts/test/OmenFactory.t.sol` (Foundry test suite TDD untuk OmenFactory)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menghemat gas onchain secara signifikan dengan hanya menyimpan hash keccak256 dari teks keyakinan, sumber URL, dan resolusi.
  - Penegakan Zero-Comment Policy dipatuhi 100% pada seluruh file smart contract Solidity.
