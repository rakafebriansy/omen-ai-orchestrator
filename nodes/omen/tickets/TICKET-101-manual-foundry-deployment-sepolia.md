---
id: TICKET-101
title: (MANUAL) Deployment Smart Contract ke Ethereum Sepolia Testnet & Verifikasi Etherscan
status: In Progress (Pending Manual Action)
priority: High
labels: [SmartContract, Foundry, Deployment, EthereumSepolia, ManualAction]
---

# Deskripsi
Setelah seluruh pengujian simulasi mock dan test suite lokal tuntas, langkah peluncuran on-chain publik adalah mendeploy smart contract `OmenFactory` dan `OmenMarket` ke jaringan testnet publik **Ethereum Sepolia (Chain ID: `11155111`)** serta memverifikasi source code di Etherscan.

Tiket ini mencakup pembuatan script deployment Foundry (`DeploySepolia.s.sol`), penyediaan private key wallet deployer ber-faucet Sepolia ETH oleh Developer, eksekusi broadcast transaksi on-chain, serta pembaruan mapping alamat kontrak live pada `omen/web/.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent menyusun script deployment Foundry pada `omen/contracts/script/DeploySepolia.s.sol`.
- [x] AI Agent menyiapkan konfigurasi network Sepolia dan template `.env.example` di `omen/contracts/`.
- [ ] **(Manual Developer)** Developer menyiapkan private key wallet deployer dan saldo Sepolia ETH (via faucet).
- [ ] **(Manual Developer)** Developer mengeksekusi script deployment: `forge script script/DeploySepolia.s.sol:DeploySepolia --rpc-url sepolia --broadcast --verify`.
- [ ] **(Manual Developer)** Developer memverifikasi transaksi deployment di Sepolia Etherscan (`https://sepolia.etherscan.io`).
- [ ] **(Manual Developer)** Developer mengisi `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA` pada `omen/web/.env.local` dengan alamat kontrak live.
- [x] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeploySepolia.s.sol`
- `omen/contracts/.env`
- `omen/web/.env.local`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menyusun script deployment Foundry pada `omen/contracts/script/DeploySepolia.s.sol` untuk menginstansiasi `OmenFactory` di Ethereum Sepolia.
  2. Mengkompilasi smart contract via `forge build` dan memvalidasi script deployment siap dieksekusi secara on-chain.
  3. Mengonfigurasi parameter rpc endpoint Sepolia dan verifier Etherscan pada `omen/contracts/foundry.toml`.
  4. Memverifikasi seluruh pengujian vitest, typecheck `tsc`, dan linter lolos 100%.
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/script/DeploySepolia.s.sol`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Script deployment mendukung opsi `--verify` untuk verifikasi otomatis kontrak cerdas di Sepolia Etherscan menggunakan API key Etherscan.
