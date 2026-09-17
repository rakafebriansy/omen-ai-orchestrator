---
id: TICKET-102
title: (MANUAL) Deployment Smart Contract ke Robinhood Chain Testnet (Chain ID 46630)
status: In Progress (Pending Manual Action)
priority: High
labels: [SmartContract, Deployment, RobinhoodChain, ManualAction, ProductionReady]
---

# Deskripsi
Setelah seluruh pengujian simulasi mock dan test suite lokal tuntas, langkah peluncuran on-chain publik ke Robinhood Chain adalah mendeploy smart contract `OmenFactory` dan `OmenMarket` ke jaringan testnet publik **Robinhood Chain Testnet (Chain ID: `46630`)** serta memverifikasi source code di Blockscout explorer.

Tiket ini mencakup penyediaan private key wallet deployer ber-faucet Robinhood Testnet ETH oleh Developer, eksekusi broadcast transaksi on-chain menggunakan script Foundry (`DeployRobinhood.s.sol`), verifikasi pada Blockscout explorer, serta pembaruan mapping alamat kontrak live pada `omen/web/.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol`.
- [x] AI Agent menyiapkan konfigurasi network Robinhood Chain Testnet di `foundry.toml`.
- [ ] **(Manual Developer)** Developer menyiapkan private key wallet deployer dan saldo Robinhood Chain Testnet ETH (via faucet resmi Robinhood Chain).
- [ ] **(Manual Developer)** Developer mengeksekusi script deployment: `forge script script/DeployRobinhood.s.sol:DeployRobinhood --rpc-url robinhood_testnet --broadcast`.
- [ ] **(Manual Developer)** Developer memverifikasi transaksi deployment di Blockscout explorer (`https://explorer.testnet.chain.robinhood.com`).
- [ ] **(Manual Developer)** Developer mengisi `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD` pada `omen/web/.env.local` dengan alamat kontrak live.
- [x] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeployRobinhood.s.sol`
- `omen/contracts/foundry.toml`
- `omen/web/.env.local`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol` untuk mendeploy `OmenFactory` ke Robinhood Chain Testnet.
  2. Mengkompilasi smart contract via `forge build` dan memvalidasi script lolos kompilasi tanpa error dengan solc 0.8.24.
  3. Mengonfigurasi endpoint RPC `https://rpc.testnet.chain.robinhood.com` dan Blockscout API verifier di `foundry.toml`.
  4. Menunggu tindakan manual Developer untuk eksekusi broadcast on-chain dengan private key ber-faucet.
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/script/DeployRobinhood.s.sol`
  - `omen/contracts/foundry.toml`
  - `omen/web/.env.local`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Script deployment siap dieksekusi kapan saja Developer memiliki saldo faucet Robinhood Testnet ETH.
