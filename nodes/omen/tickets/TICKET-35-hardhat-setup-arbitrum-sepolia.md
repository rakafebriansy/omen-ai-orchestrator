---
id: TICKET-35
title: Inisialisasi Hardhat dan Konfigurasi Arbitrum Sepolia
status: Done
priority: High
labels: [SmartContract, Tooling]
---

# Deskripsi
Menginisialisasi framework pengembangan smart contract Hardhat TypeScript di direktori `omen/contracts`, memasang OpenZeppelin Contracts, dan mengonfigurasi jaringan testnet Arbitrum Sepolia.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Konfigurasi Hardhat
- Framework: Hardhat dengan `@nomicfoundation/hardhat-toolbox`.
- Dependensi: `@openzeppelin/contracts` versi ^5.0.0 (Ownable, ReentrancyGuard).
- Network Config: `arbitrumSepolia` (Chain ID 421614, RPC `SEPOLIA_RPC_URL`, accounts `PRIVATE_KEY`).
- Compiler: Solidity 0.8.20 dengan optimizer aktif (200 runs).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Folder omen/contracts terkonfigurasi dengan package.json, tsconfig.json, dan hardhat.config.ts.
- [x] Dependensi OpenZeppelin terpasang dan siap diimpor.
- [x] Perintah npx hardhat compile berjalan sukses tanpa peringatan.

## Target Lingkup File (Affected Files)
- `omen/contracts/package.json`
- `omen/contracts/hardhat.config.ts`
- `omen/contracts/tsconfig.json`
- `omen/contracts/.env.example`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat branch baru `feat/contracts` pada repositori `omen` sesuai evaluasi domain fitur Smart Contract & Web3.
  2. Mengonfigurasi `package.json` di direktori `omen/contracts` dengan dependensi Hardhat v2, `@nomicfoundation/hardhat-toolbox` v5, `@openzeppelin/contracts` v5, `dotenv`, dan TypeScript tooling.
  3. Mengonfigurasi `tsconfig.json` untuk dukungan TypeScript pada Hardhat scripts, tests, dan config.
  4. Mengimplementasikan `hardhat.config.ts` dengan jaringan Arbitrum Sepolia (Chain ID 421614, RPC dari env, optimizer 200 runs) dengan kepatuhan mutlak Zero-Comment Policy.
  5. Membuat file `.env.example` sebagai referensi konfigurasi variabel lingkungan RPC dan private key.
  6. Menjalankan instalasi `npm install` di `omen/contracts`.
  7. Menjalankan kompilasi `npx hardhat compile` (sukses tanpa peringatan).
  8. Menjalankan validasi TypeScript `npx tsc --noEmit` (lolos tanpa error).
  9. Menjalankan suite pengujian web `npm run test` di `omen/web` (seluruh 127 pengujian di 22 file tetap 100% pass).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/package.json`
  - `omen/contracts/package-lock.json`
  - `omen/contracts/tsconfig.json`
  - `omen/contracts/hardhat.config.ts`
  - `omen/contracts/.env.example`
  - `nodes/omen/tickets/TICKET-35-hardhat-setup-arbitrum-sepolia.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengisolasi dependensi Hardhat di dalam direktori `omen/contracts` untuk mencegah konflik versi dengan Next.js 16/React 19 di `omen/web`.
  - Mengonfigurasi network Arbitrum Sepolia dengan fallback RPC resmi Arbitrum (`https://sepolia-rollup.arbitrum.io/rpc`) jika `SEPOLIA_RPC_URL` tidak diisi.
