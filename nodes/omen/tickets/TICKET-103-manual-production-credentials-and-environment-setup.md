---
id: TICKET-103
title: (MANUAL) Penyediaan Kredensial Nyata & Konfigurasi Environment Production (.env.local)
status: In Progress (Pending Manual Configuration)
priority: High
labels: [DevOps, Security, Configuration, ManualAction, ProductionReady]
---

# Deskripsi
Setelah seluruh simulasi mock dan verifikasi trust checklist pada TICKET-100 terpenuhi, langkah akhir sebelum peluncuran on-chain publik adalah penyediaan kredensial asli dan live secrets ke dalam file lingkungan lokal (`omen/web/.env.local` dan `omen/contracts/.env`).

Tiket ini mencakup penyediaan API key nyata untuk AI LLM extractor (OpenRouter), private key akun server-side admin/resolver dengan saldo gas ETH testnet, RPC endpoint berbayar/publik berkecepatan tinggi, serta alamat smart contract live hasil deployment TICKET-101 (Sepolia) dan TICKET-102 (Robinhood Chain Testnet).

Cakupan Variabel Lingkungan Nyata (.env.local):
```env
NEXT_PUBLIC_CHAIN_ENV=testnet
NEXT_PUBLIC_USE_MOCK_CONTRACT=false

# Multi-Chain RPC Endpoints
NEXT_PUBLIC_ETH_SEPOLIA_RPC=https://eth-sepolia.g.alchemy.com/v2/YOUR_ALCHEMY_KEY
NEXT_PUBLIC_ROBINHOOD_TESTNET_RPC=https://rpc.testnet.chain.robinhood.com
NEXT_PUBLIC_ROBINHOOD_CHAIN_ID=46630

# Live Smart Contract Factory Addresses (Setelah TICKET-101 & TICKET-102)
NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA=0x...
NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD=0x...

# Chainlink AggregatorV3 Feeds (Sepolia)
NEXT_PUBLIC_CHAINLINK_ETH_USD_FEED=0x694AA1769357215DE4FAC081bf1f309aDC325306
NEXT_PUBLIC_CHAINLINK_BTC_USD_FEED=0x1b44F3514812d835EB1BDB0acB33d3fA3351Ee43
NEXT_PUBLIC_CHAINLINK_SOL_USD_FEED=0xC5981F461d74c46eB4b0CF3f4Ec79f025573B0Ea

# AI Model Extraction Keys (Server-side)
AI_API_KEY=sk-or-v1-YOUR_OPENROUTER_API_KEY
AI_MODEL=meta-llama/llama-3.3-70b-instruct:free

# Server-Side Oracle & Market Admin Key (Dengan saldo ETH untuk submit on-chain)
ADMIN_PRIVATE_KEY=0xYOUR_SERVER_WALLET_PRIVATE_KEY
```

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent menyiapkan dokumentasi format environment variables dan trust security checklist.
- [ ] **(Manual Developer)** Developer menyediakan `AI_API_KEY` OpenRouter nyata pada `omen/web/.env.local`.
- [ ] **(Manual Developer)** Developer mengisi `ADMIN_PRIVATE_KEY` dengan wallet yang memiliki saldo testnet ETH.
- [ ] **(Manual Developer)** Developer memasukkan alamat `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA` (dari TICKET-101) dan `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD` (dari TICKET-102).
- [ ] **(Manual Developer)** Developer menguji koneksi langsung ke smart contract live dengan menyetel `NEXT_PUBLIC_USE_MOCK_CONTRACT=false`.
- [x] Memastikan tidak ada secret/API key nyata yang terekspos ke bundle browser client (`NEXT_PUBLIC_`).
- [x] Memverifikasi kelulusan 100% build Next.js (`npm run build`) dan TypeScript typecheck (`tsc --noEmit`).

## Target Lingkup File (Affected Files)
- `omen/web/.env.local`
- `omen/contracts/.env`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengisolasi seluruh kebutuhan konfigurasi kredensial nyata ke tiket khusus TICKET-103.
  2. Menyusun panduan variabel lingkungan production-ready untuk integrasi live on-chain.
- **Ringkasan File Terpengaruh:**
  - `omen/web/.env.local`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Aplikasi siap dialihkan ke mode live on-chain murni seketika Developer mengisi `.env.local` dan menyetel `NEXT_PUBLIC_USE_MOCK_CONTRACT=false`.
