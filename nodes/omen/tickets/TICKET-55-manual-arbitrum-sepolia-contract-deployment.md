---
id: TICKET-55
title: (MANUAL) Deployment Smart Contract ke Arbitrum Sepolia Testnet & Verifikasi Arbiscan
status: Todo
priority: High
labels: [SmartContract, Blockchain, ManualAction, Arbitrum, Deployment]
---

# Deskripsi
Smart contract `PredictionMarket.sol` telah selesai dikembangkan dan diuji pada Hardhat unit test lokal. Untuk menghubungkan platform web dengan testnet publik nyata, deployer wallet developer membutuhkan dana faucet Arbitrum Sepolia ETH untuk mengeksekusi script deployment `contracts/scripts/deploy.ts` dan mengonfigurasi contract address publik di `.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Developer menyiapkan wallet deployer dengan saldo testnet Arbitrum Sepolia ETH (via faucet).
- [ ] Mengisi variabel lingkungan di `omen/contracts/.env`:
  - `ARBITRUM_SEPOLIA_RPC_URL` (contoh: `https://sepolia-rollup.arbitrum.io/rpc`)
  - `PRIVATE_KEY` atau `MNEMONIC` (deployer credentials)
  - `ARBISCAN_API_KEY` (opsional untuk verifikasi source code)
- [ ] Menjalankan perintah migrasi on-chain: `npm run deploy:arbitrum-sepolia --prefix contracts`.
- [ ] Memastikan file `web/lib/contracts.ts` dan `web/contracts/PredictionMarket.json` terupdate dengan alamat kontrak baru.
- [ ] Mengisi variabel lingkungan `NEXT_PUBLIC_PREDICTION_MARKET_ADDRESS` dan `NEXT_PUBLIC_ADMIN_WALLET_ADDRESS` pada `omen/web/.env.local`.

## Target Lingkup File (Affected Files)
- `omen/contracts/.env`
- [deploy.ts:L1](../../../../omen/contracts/scripts/deploy.ts#L1)
- `omen/web/.env.local`
- [contracts.ts:L1](../../../../omen/web/lib/contracts.ts#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menunggu tindakan manual developer untuk eksekusi deployment on-chain nyata.
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/.env`, `omen/web/.env.local`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Dipindahkan ke Tahap 6 pasca penyelesaian validasi simulator dan integrasi Supabase.
