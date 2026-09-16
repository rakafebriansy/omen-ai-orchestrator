---
id: TICKET-71
title: Script Deployment Foundry Ethereum Sepolia & Ekspor Artefak ABI ke Web
status: Todo
priority: High
labels: [SmartContract, Foundry, Deployment, Web3]
---

# Deskripsi
Setelah smart contract `OmenFactory` dan `OmenMarket` tervalidasi di lingkungan pengujian, langkah berikutnya adalah menyusun skrip deployment Foundry berbasis Solidity Script (`forge script`) dan mengekspor artefak ABI ke modul frontend `omen/web`.

Tiket ini mencakup pembuatan skrip deployment ke jaringan Ethereum Sepolia, export ABI file JSON ke `omen/web/contracts/`, serta pembaruan konstanta konfigurasi kontrak pada `omen/web/lib/contracts.ts`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyusun script deployment Foundry pada `omen/contracts/script/DeploySepolia.s.sol`.
- [ ] Menyediakan mekanisme ekspor ABI `OmenFactory.json` dan `OmenMarket.json` ke direktori `omen/web/contracts/`.
- [ ] Memperbarui `omen/web/lib/contracts.ts` dengan ABI terdefinisi `as const` (untuk Wagmi type safety) dan mapping contract address per chain ID (Sepolia: `11155111`, Robinhood Testnet: `46630`).
- [ ] Menyiapkan variabel lingkungan `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA` pada `omen/web/.env.example`.
- [ ] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeploySepolia.s.sol`
- `omen/web/contracts/OmenFactory.json`
- `omen/web/contracts/OmenMarket.json`
- `omen/web/lib/contracts.ts`
- `omen/web/.env.example`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
