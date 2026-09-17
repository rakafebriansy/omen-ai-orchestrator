---
id: TICKET-71
title: Setup Mock Smart Contract Environment, Ekspor Artefak ABI ke Web & Konfigurasi Contracts Helper
status: Done
priority: High
labels: [SmartContract, Foundry, MockEnvironment, Web3, Tooling]
---

# Deskripsi
Setelah smart contract `OmenFactory` dan `OmenMarket` tervalidasi di lingkungan pengujian Foundry lokal, artefak ABI murni perlu diekspor ke modul frontend `omen/web` serta mengonfigurasi *Mock Smart Contract Environment* agar pengembangan frontend/client dapat berjalan instan tanpa ketergantungan pada faucet jaringan testnet publik.

Tiket ini mencakup kompilasi kontrak via Foundry (`forge build`), ekspor ABI `OmenFactory.json` dan `OmenMarket.json` ke `omen/web/contracts/`, konfigurasi konstanta alamat fallback mock (`0x1111111111111111111111111111111111111111` & `USE_MOCK_CONTRACT = true`) pada `omen/web/lib/contracts.ts`, serta penyusunan unit test validasi ABI.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent mengompilasi smart contract Foundry (`forge build`) dan memverifikasi integritas bytecode serta interface.
- [x] AI Agent mengekspor artefak ABI `OmenFactory.json` dan `OmenMarket.json` ke direktori `omen/web/contracts/`.
- [x] AI Agent memperbarui `omen/web/lib/contracts.ts` dengan ekspor ABI terdefinisi modular serta konstanta alamat multi-chain dengan fallback mock address (`0x1111111111111111111111111111111111111111`).
- [x] AI Agent memastikan flag `USE_MOCK_CONTRACT` aktif secara default untuk mendukung simulasi transaksi gasless lokal pada hook `useCreateMarket`, `usePosition`, dan `useClaim`.
- [x] Menyusun unit test validasi ekspor ABI pada `omen/web/tests/contracts-abi.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.
- [x] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/web/contracts/OmenFactory.json`
- `omen/web/contracts/OmenMarket.json`
- `omen/web/lib/contracts.ts`
- `omen/web/tests/contracts-abi.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Mengkompilasi smart contract dengan Foundry (`forge build`) dan mengekstrak ABI murni ke `omen/web/contracts/OmenFactory.json` dan `omen/web/contracts/OmenMarket.json`.
  2. Memperbarui `omen/web/lib/contracts.ts` dengan export `OMEN_FACTORY_ABI`, `OMEN_MARKET_ABI`, `OMEN_FACTORY_ADDRESS_SEPOLIA`, `OMEN_FACTORY_ADDRESS_ROBINHOOD`, fallback `OMEN_FACTORY_ADDRESS` mock address `0x1111111111111111111111111111111111111111`, helper `getOmenFactoryAddress`, serta `USE_MOCK_CONTRACT`.
  3. Menyusun unit test pada `omen/web/tests/contracts-abi.test.ts` untuk memverifikasi struktur fungsi ABI, fungsi resolusi alamat multi-chain, dan Zero-Comment Policy.
  4. Menjalankan pengujian vitest (376 tests pass di 73 test files), typecheck `tsc --noEmit`, dan linter ESLint (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/contracts/OmenFactory.json`
  - `omen/web/contracts/OmenMarket.json`
  - `omen/web/lib/contracts.ts`
  - `omen/web/tests/contracts-abi.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - ABI diekspor ke format JSON modular dan diimpor langsung oleh `omen/web/lib/contracts.ts` dengan integrasi `resolveJsonModule` TypeScript untuk sinkronisasi otomatis tipe Wagmi/Viem saat smart contract diperbarui.
  - Mock contract environment aktif secara otomatis sehingga seluruh flow transaksi UI dapat diverifikasi tanpa jeda transaksi blockchain live.
