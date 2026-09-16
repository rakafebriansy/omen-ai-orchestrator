---
id: TICKET-67
title: Inisialisasi Lingkungan Foundry & Konfigurasi Multi-Chain
status: Todo
priority: High
labels: [SmartContract, Foundry, MultiChain]
---

# Deskripsi
OMEN V1 beralih ke Foundry sebagai toolkit pengembangan smart contract utama untuk memastikan eksekusi tes yang cepat, fuzzed testing bawaan, dan deployment deterministik.

Tiket ini mencakup setup proyek Foundry di `omen/contracts/`, instalasi pustaka OpenZeppelin Contracts v5 via git submodule / `forge install`, penyusunan `foundry.toml` dengan profil multi-chain (Ethereum Sepolia dan Robinhood Chain Testnet 46630), serta pemetaan `remappings.txt`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyiapkan file konfigurasi `foundry.toml` di `omen/contracts/` dengan pengaturan solc optimizer (200 runs), evm_version (cancun / paris), dan rpc_endpoints untuk `sepolia` dan `robinhood_testnet`.
- [ ] Menginstal dependency OpenZeppelin Contracts v5 (`@openzeppelin/contracts`) di dalam `omen/contracts/lib/` atau remappings yang valid.
- [ ] Menyiapkan file `remappings.txt` dan `.env.example` untuk kredensial RPC URL, Private Key deployer, dan Etherscan/Blockscout API keys.
- [ ] Memastikan `forge build` dapat dieksekusi tanpa error.
- [ ] Menyediakan dokumentasi instruksi instalasi dan build di `omen/contracts/README.md`.

## Target Lingkup File (Affected Files)
- `omen/contracts/foundry.toml`
- `omen/contracts/remappings.txt`
- `omen/contracts/.env.example`
- `omen/contracts/README.md`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
