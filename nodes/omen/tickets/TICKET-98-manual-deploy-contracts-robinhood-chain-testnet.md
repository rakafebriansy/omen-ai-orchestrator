---
id: TICKET-98
title: (MANUAL) Deployment Smart Contract ke Robinhood Chain Testnet (Chain ID 46630)
status: Done
priority: High
labels: [SmartContract, Deployment, RobinhoodChain, ManualAction]
---

# Deskripsi
Setelah validasi di Ethereum Sepolia tuntas, smart contract `OmenFactory` dan `OmenMarket` perlu dideploy ke **Robinhood Chain Testnet (Chain ID 46630)** sesuai spesifikasi arsitektur dual-testnet OMEN V1.

Tiket ini mencakup pembuatan script deployment Foundry (`DeployRobinhood.s.sol`), konfigurasi RPC endpoint `https://rpc.testnet.chain.robinhood.com`, eksekusi manual on-chain deployment oleh Developer dengan wallet ber-faucet Robinhood Testnet ETH, verifikasi pada Blockscout explorer, serta pembaruan mapping alamat kontrak pada `omen/web/lib/contracts.ts` dan `.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol`.
- [x] AI Agent menyiapkan konfigurasi network Robinhood Chain Testnet di `foundry.toml`.
- [x] **(Manual Developer)** Developer menyiapkan private key wallet deployer dan saldo Robinhood Chain Testnet ETH (via faucet).
- [x] **(Manual Developer)** Developer mengeksekusi script deployment: `forge script script/DeployRobinhood.s.sol:DeployRobinhood --rpc-url robinhood_testnet --broadcast`.
- [x] **(Manual Developer)** Developer memverifikasi transaksi deployment di Blockscout explorer (`https://explorer.testnet.chain.robinhood.com`).
- [x] AI Agent memperbarui `omen/web/lib/contracts.ts` dengan alamat kontrak `OmenFactory` untuk Chain ID 46630.
- [x] **(Manual Developer)** Developer mengisi `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD` pada `omen/web/.env.local`.
- [x] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeployRobinhood.s.sol`
- `omen/contracts/foundry.toml`
- `omen/web/lib/contracts.ts`
- `omen/web/.env.local`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol` untuk mendeploy `OmenFactory` ke Robinhood Chain Testnet.
  2. Mengkompilasi smart contract via `forge build` untuk memastikan script lolos kompilasi tanpa error.
  3. Memastikan pemetaan konstanta `ROBINHOOD_TESTNET_CHAIN_ID = 46630`, `OMEN_FACTORY_ADDRESS_ROBINHOOD`, dan helper `getOmenFactoryAddress` di `omen/web/lib/contracts.ts`.
  4. Menyusun unit test TDD pada `omen/web/tests/contracts-robinhood-deploy.test.ts` dan memverifikasi kepatuhan Zero-Comment Policy.
  5. Menjalankan pengujian vitest (323 tests pass di 57 test files), typecheck `tsc`, dan linter ESLint (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/script/DeployRobinhood.s.sol`
  - `omen/web/tests/contracts-robinhood-deploy.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Konfigurasi RPC Robinhood Chain Testnet (`https://rpc.testnet.chain.robinhood.com`) terdaftar di `foundry.toml` dengan opsi verifikasi blockscout explorer API untuk mendukung verifikasi source code on-chain.
