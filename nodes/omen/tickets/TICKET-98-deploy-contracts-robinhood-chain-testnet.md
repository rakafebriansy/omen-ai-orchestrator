---
id: TICKET-98
title: Deployment Smart Contract ke Robinhood Chain Testnet (Chain ID 46630)
status: Todo
priority: High
labels: [SmartContract, Deployment, RobinhoodChain]
---

# Deskripsi
Setelah validasi di Ethereum Sepolia tuntas, smart contract `OmenFactory` dan dependensinya perlu dideploy ke **Robinhood Chain Testnet (Chain ID 46630)** sesuai spesifikasi arsitektur dual testnet OMEN V1.

Langkah-langkah yang tercakup:
1. Menyusun skrip deployment Foundry `omen/contracts/script/DeployRobinhood.s.sol`.
2. Mengonfigurasi RPC endpoint `https://rpc.testnet.chain.robinhood.com` dan block explorer Blockscout `https://explorer.testnet.chain.robinhood.com`.
3. Memperbarui mapping alamat kontrak pada `omen/web/lib/contracts.ts` agar mendukung multi-chain lookup secara dinamis berdasarkan `chainId`.
4. Mengonfigurasi variabel lingkungan `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD` pada `.env.example` dan `.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol`.
- [ ] Menyiapkan konfigurasi network Robinhood Chain Testnet di `foundry.toml`.
- [ ] Memperbarui `omen/web/lib/contracts.ts` dengan alamat kontrak OmenFactory untuk Chain ID 46630.
- [ ] Memastikan seluruh artefak build dan ABI kontrak tersinkronisasi.
- [ ] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeployRobinhood.s.sol`
- `omen/contracts/foundry.toml`
- `omen/web/lib/contracts.ts`
- `omen/web/.env.example`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
