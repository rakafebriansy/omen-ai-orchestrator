---
id: TICKET-67
title: Inisialisasi Lingkungan Foundry & Konfigurasi Multi-Chain
status: Done
priority: High
labels: [SmartContract, Foundry, MultiChain]
---

# Deskripsi
OMEN V1 beralih ke Foundry sebagai toolkit pengembangan smart contract utama untuk memastikan eksekusi tes yang cepat, fuzzed testing bawaan, dan deployment deterministik.

Tiket ini mencakup setup proyek Foundry di `omen/contracts/`, instalasi pustaka OpenZeppelin Contracts v5 via git submodule / `forge install`, penyusunan `foundry.toml` dengan profil multi-chain (Ethereum Sepolia dan Robinhood Chain Testnet 46630), serta pemetaan `remappings.txt`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menyiapkan file konfigurasi `foundry.toml` di `omen/contracts/` dengan pengaturan solc optimizer (200 runs), evm_version (cancun / paris), dan rpc_endpoints untuk `sepolia` dan `robinhood_testnet`.
- [x] Menginstal dependency OpenZeppelin Contracts v5 (`@openzeppelin/contracts`) di dalam `omen/contracts/lib/` atau remappings yang valid.
- [x] Menyiapkan file `remappings.txt` dan `.env.example` untuk kredensial RPC URL, Private Key deployer, dan Etherscan/Blockscout API keys.
- [x] Memastikan `forge build` dapat dieksekusi tanpa error.
- [x] Menyediakan dokumentasi instruksi instalasi dan build di `omen/contracts/README.md`.

## Target Lingkup File (Affected Files)
- `omen/contracts/foundry.toml`
- `omen/contracts/remappings.txt`
- `omen/contracts/.env.example`
- `omen/contracts/README.md`
- `omen/contracts/test/Sanity.t.sol`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Melakukan verifikasi dan instalasi toolchain Foundry (`forge 1.8.3`, `cast 1.8.3`) ke environment sistem.
  2. Menginstal pustaka standard testing Foundry `forge-std` ke `omen/contracts/lib/forge-std`.
  3. Mengonfigurasi `foundry.toml` dengan solc 0.8.24, optimizer 200 runs, evm_version cancun, serta RPC endpoints untuk Ethereum Sepolia dan Robinhood Chain Testnet (Chain ID 46630).
  4. Menyusun remappings di `remappings.txt` untuk mengintegrasikan `@openzeppelin/contracts/` dari `node_modules` dan `forge-std/` dari `lib/forge-std/src/`.
  5. Menulis template variabel lingkungan di `omen/contracts/.env.example` dan dokumentasi Foundry di `omen/contracts/README.md`.
  6. Menulis test sanity TDD di `omen/contracts/test/Sanity.t.sol` untuk memvalidasi kompilasi, impor forge-std, dan integrasi OpenZeppelin.
  7. Menjalankan `forge test -vv` dengan hasil 100% PASS (2 passed, 0 failed).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/foundry.toml` (Konfigurasi profil multi-chain, RPC, dan optimizer Foundry)
  - `omen/contracts/remappings.txt` (Pemetaan path OpenZeppelin dan forge-std)
  - `omen/contracts/.env.example` (Template konfigurasi RPC & API keys Sepolia & Robinhood)
  - `omen/contracts/README.md` (Dokumentasi build & testing instruksi Foundry)
  - `omen/contracts/test/Sanity.t.sol` (Test sanity kompilasi dan dependensi)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan resolusi `node_modules/@openzeppelin/contracts` untuk konsistensi dependensi npm mono-repo dan kompatibilitas seamless dengan script Hardhat/Typechain yang sudah ada.
  - Penegakan aturan Zero-Comment dipatuhi pada seluruh file konfigurasi dan test contract.
