---
id: TICKET-68
title: Implementasi Smart Contract OmenFactory.sol
status: Todo
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
- [ ] Mengimplementasikan `OmenFactory.sol` di `omen/contracts/src/OmenFactory.sol`.
- [ ] Menyediakan fungsi `createMarket(bytes32 beliefHash, bytes32 sourceHash, bytes32 resolutionHash, uint256 openTime, uint256 closeTime, ResolutionConfig calldata config) external returns (address marketAddress)`.
- [ ] Mengimplementasikan role-based access control dengan OpenZeppelin AccessControl.
- [ ] Menyediakan event `MarketCreated(uint256 indexed marketId, address indexed marketAddress, bytes32 indexed beliefHash, uint256 closeTime)`.
- [ ] Menyediakan getter helpers: `getMarket(uint256 marketId)`, `totalMarkets()`, `isMarketValid(address marketAddress)`.
- [ ] Mematuhi Zero-Comment Policy dan lulus kompilasi `forge build` 100%.

## Target Lingkup File (Affected Files)
- `omen/contracts/src/OmenFactory.sol`
- `omen/contracts/src/interfaces/IOmenFactory.sol`
- `omen/contracts/src/types/MarketTypes.sol`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
