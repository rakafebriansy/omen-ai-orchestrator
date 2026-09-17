---
id: TICKET-71
title: (MANUAL) Deployment Smart Contract ke Ethereum Sepolia & Ekspor Artefak ABI ke Web
status: Todo
priority: High
labels: [SmartContract, Foundry, Deployment, Web3, ManualAction]
---

# Deskripsi
Setelah smart contract `OmenFactory` dan `OmenMarket` tervalidasi di lingkungan pengujian lokal, langkah berikutnya adalah mendeploy kontrak ke jaringan testnet publik Ethereum Sepolia (`11155111`) dan mengekspor artefak ABI ke modul frontend `omen/web`.

Tiket ini mencakup pembuatan script deployment Foundry (`DeploySepolia.s.sol`), eksekusi manual on-chain deployment oleh Developer dengan wallet deployer ber-faucet Sepolia ETH, ekspor ABI ke `omen/web/contracts/`, serta pembaruan konstanta alamat kontrak pada `omen/web/lib/contracts.ts`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] AI Agent menyusun script deployment Foundry pada `omen/contracts/script/DeploySepolia.s.sol`.
- [ ] AI Agent menyiapkan konfigurasi network dan template `.env.example` di `omen/contracts/`.
- [ ] **(Manual Developer)** Developer menyiapkan private key wallet deployer dan saldo Sepolia ETH (via faucet).
- [ ] **(Manual Developer)** Developer mengeksekusi script deployment: `forge script DeploySepolia --rpc-url sepolia --broadcast --verify`.
- [ ] AI Agent mengekspor artefak ABI `OmenFactory.json` dan `OmenMarket.json` ke direktori `omen/web/contracts/`.
- [ ] AI Agent memperbarui `omen/web/lib/contracts.ts` dengan ABI terdefinisi `as const` dan mapping alamat kontrak `OmenFactory` Sepolia.
- [ ] **(Manual Developer)** Developer mengisi `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA` pada `omen/web/.env.local`.
- [ ] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeploySepolia.s.sol`
- `omen/contracts/.env`
- `omen/web/contracts/OmenFactory.json`
- `omen/web/contracts/OmenMarket.json`
- `omen/web/lib/contracts.ts`
- `omen/web/.env.local`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
