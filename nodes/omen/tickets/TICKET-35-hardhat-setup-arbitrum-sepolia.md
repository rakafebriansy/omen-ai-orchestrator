---
id: TICKET-35
title: Inisialisasi Hardhat dan Konfigurasi Arbitrum Sepolia
status: Todo
priority: High
labels: [SmartContract, Tooling]
---

# Deskripsi
Menginisialisasi framework pengembangan smart contract Hardhat TypeScript di direktori `omen/contracts`, memasang OpenZeppelin Contracts, dan mengonfigurasi jaringan testnet Arbitrum Sepolia.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Konfigurasi Hardhat
- Framework: Hardhat dengan `@nomicfoundation/hardhat-toolbox`.
- Dependensi: `@openzeppelin/contracts` versi ^5.0.0 (Ownable, ReentrancyGuard).
- Network Config: `arbitrumSepolia` (Chain ID 421614, RPC `SEPOLIA_RPC_URL`, accounts `PRIVATE_KEY`).
- Compiler: Solidity 0.8.20 dengan optimizer aktif (200 runs).

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Folder omen/contracts terkonfigurasi dengan package.json, tsconfig.json, dan hardhat.config.ts.
- [ ] Dependensi OpenZeppelin terpasang dan siap diimpor.
- [ ] Perintah npx hardhat compile berjalan sukses tanpa peringatan.

## Target Lingkup File (Affected Files)
- `omen/contracts/package.json`
- `omen/contracts/hardhat.config.ts`
- `omen/contracts/tsconfig.json`
- `omen/contracts/.env.example`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
