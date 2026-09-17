---
id: TICKET-98
title: (MANUAL) Deployment Smart Contract ke Robinhood Chain Testnet (Chain ID 46630)
status: Todo
priority: High
labels: [SmartContract, Deployment, RobinhoodChain, ManualAction]
---

# Deskripsi
Setelah validasi di Ethereum Sepolia tuntas, smart contract `OmenFactory` dan `OmenMarket` perlu dideploy ke **Robinhood Chain Testnet (Chain ID 46630)** sesuai spesifikasi arsitektur dual-testnet OMEN V1.

Tiket ini mencakup pembuatan script deployment Foundry (`DeployRobinhood.s.sol`), konfigurasi RPC endpoint `https://rpc.testnet.chain.robinhood.com`, eksekusi manual on-chain deployment oleh Developer dengan wallet ber-faucet Robinhood Testnet ETH, verifikasi pada Blockscout explorer, serta pembaruan mapping alamat kontrak pada `omen/web/lib/contracts.ts` dan `.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] AI Agent menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol`.
- [ ] AI Agent menyiapkan konfigurasi network Robinhood Chain Testnet di `foundry.toml`.
- [ ] **(Manual Developer)** Developer menyiapkan private key wallet deployer dan saldo Robinhood Chain Testnet ETH (via faucet).
- [ ] **(Manual Developer)** Developer mengeksekusi script deployment: `forge script DeployRobinhood --rpc-url robinhood_testnet --broadcast`.
- [ ] **(Manual Developer)** Developer memverifikasi transaksi deployment di Blockscout explorer (`https://explorer.testnet.chain.robinhood.com`).
- [ ] AI Agent memperbarui `omen/web/lib/contracts.ts` dengan alamat kontrak `OmenFactory` untuk Chain ID 46630.
- [ ] **(Manual Developer)** Developer mengisi `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD` pada `omen/web/.env.local`.
- [ ] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeployRobinhood.s.sol`
- `omen/contracts/foundry.toml`
- `omen/web/lib/contracts.ts`
- `omen/web/.env.local`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
