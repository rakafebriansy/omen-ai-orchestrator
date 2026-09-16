---
id: TICKET-38
title: Script Deployment Testnet dan Ekspor ABI
status: Done
priority: High
labels: [SmartContract, DevOps]
---

# Deskripsi
Membuat script deployment di `omen/contracts/scripts/deploy.ts` untuk mendeploy kontrak ke Arbitrum Sepolia dan mengekspor alamat kontrak beserta ABI ke frontend `omen/web/lib/contracts.ts`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Deployment Script
- Script `scripts/deploy.ts` mendeploy `PredictionMarket.sol` menggunakan signer deployer.
- Script menuliskan alamat kontrak aktif dan file ABI JSON ke `omen/web/lib/contracts.ts`.
- Menyertakan instruksi verifikasi kontrak di block explorer Arbiscan Sepolia.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Script deploy.ts berhasil mengeksekusi migrasi kontrak ke testnet.
- [x] Berkas omen/web/lib/contracts.ts memuat ABI final dan alamat kontrak aktif.
- [x] Dokumentasi deployment testnet tercatat di README.

## Target Lingkup File (Affected Files)
- `omen/contracts/scripts/deploy.ts`
- `omen/contracts/README.md`
- `omen/web/lib/contracts.ts`
- `omen/web/contracts/PredictionMarket.json`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan script deployment TypeScript `omen/contracts/scripts/deploy.ts` yang menginisialisasi signer deployer, mendeploy `PredictionMarket.sol`, menunggu konfirmasi on-chain, dan mencetak instruksi verifikasi Arbiscan Sepolia.
  2. Mengotomatisasi ekspor artefak ABI dan contract address dari build artifacts ke dua lokasi target:
     - `omen/web/lib/contracts.ts`: typed contract configuration dengan `as const` untuk integrasi type-safe Wagmi/Viem, `ARBITRUM_SEPOLIA_CHAIN_ID = 421614`, serta fallback env `NEXT_PUBLIC_PREDICTION_MARKET_ADDRESS`.
     - `omen/web/contracts/PredictionMarket.json`: file JSON ABI lengkap untuk interoperabilitas Web3 tooling.
  3. Menyusun dokumentasi deployment testnet dan instruksi verifikasi kontrak Arbiscan Sepolia di `omen/contracts/README.md`.
  4. Menjalankan pengujian eksekusi deployer `npx hardhat run scripts/deploy.ts` yang sukses mendeploy kontrak dan mengekspor file secara otomatis.
  5. Menjalankan validasi TypeScript `npx tsc --noEmit` di `omen/contracts` dan `omen/web` (0 errors), serta suite unit test web (127 test pass).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/scripts/deploy.ts`
  - `omen/contracts/README.md`
  - `omen/web/lib/contracts.ts`
  - `omen/web/contracts/PredictionMarket.json`
  - `nodes/omen/tickets/TICKET-38-testnet-deployment-abi-export.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menerapkan anotasi TypeScript `as const` pada definisi array ABI di `contracts.ts` agar Wagmi hooks (`useReadContract`, `useWriteContract`) mendeteksi secara otomatis typesafe nama fungsi dan argumen tanpa perlu typecasting manual.
