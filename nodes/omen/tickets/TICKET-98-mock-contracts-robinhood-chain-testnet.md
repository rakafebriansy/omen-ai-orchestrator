---
id: TICKET-98
title: Konfigurasi Mock Smart Contract & Simulasi Dual-Chain Robinhood Testnet (Chain ID 46630)
status: Done
priority: High
labels: [SmartContract, MockWeb3, RobinhoodChain, MultiChain]
---

# Deskripsi
Menyediakan integrasi mock smart contract dan simulator Web3 untuk **Robinhood Chain Testnet (Chain ID 46630)** pada arsitektur dual-testnet OMEN V1.

Tiket ini mencakup pembuatan script deployment Foundry (`DeployRobinhood.s.sol`), konfigurasi network RPC di `foundry.toml`, konfigurasi mock address fallback `MOCK_OMEN_FACTORY_ADDRESS_ROBINHOOD` pada `omen/web/lib/mockContracts.ts`, serta pemetaan resolver fungsi di `omen/web/lib/contracts.ts` agar seluruh fitur aplikasi dapat berjalan penuh tanpa ketergantungan pada wallet fisik maupun saldo faucet nyata.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol`.
- [x] AI Agent menyiapkan konfigurasi network Robinhood Chain Testnet di `foundry.toml`.
- [x] AI Agent mengonfigurasi mock fallback address `MOCK_OMEN_FACTORY_ADDRESS_ROBINHOOD` (`0x2222222222222222222222222222222222222222`) pada `omen/web/lib/mockContracts.ts`.
- [x] AI Agent memperbarui `omen/web/lib/contracts.ts` dengan resolver `getOmenFactoryAddress(46630)` dan isolasi error throwing murni.
- [x] Seluruh Web3 hooks (`usePosition`, `useClaim`, `useCreateMarket`, `useCreatorConfirm`) terintegrasi dengan simulator mock dual-chain.
- [x] Pengujian unit test dan E2E dual-chain workflow (`dual-chain-workflow.test.ts`) lulus 100%.
- [x] Memastikan `npx tsc --noEmit` di `omen/web` lulus tanpa type error.

## Target Lingkup File (Affected Files)
- `omen/contracts/script/DeployRobinhood.s.sol`
- `omen/contracts/foundry.toml`
- `omen/web/lib/contracts.ts`
- `omen/web/lib/mockContracts.ts`
- `omen/web/tests/contracts-robinhood-deploy.test.ts`
- `omen/web/tests/e2e/dual-chain-workflow.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menyusun script deployment Foundry pada `omen/contracts/script/DeployRobinhood.s.sol` untuk mendeploy `OmenFactory` ke Robinhood Chain Testnet.
  2. Mengkompilasi smart contract via `forge build` untuk memastikan script lolos kompilasi tanpa error.
  3. Mengisolasi mock address `MOCK_OMEN_FACTORY_ADDRESS_ROBINHOOD` ke `omen/web/lib/mockContracts.ts` dan menyediakan helper `getMockOmenFactoryAddress(46630)`.
  4. Memastikan pemetaan konstanta `ROBINHOOD_TESTNET_CHAIN_ID = 46630`, `OMEN_FACTORY_ADDRESS_ROBINHOOD`, dan helper `getOmenFactoryAddress` di `omen/web/lib/contracts.ts`.
  5. Menyusun unit test TDD pada `omen/web/tests/contracts-robinhood-deploy.test.ts` dan E2E multi-chain test pada `omen/web/tests/e2e/dual-chain-workflow.test.ts`.
  6. Memverifikasi seluruh pengujian vitest (379 tests pass di 73 test files), typecheck `tsc`, dan linter ESLint (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/script/DeployRobinhood.s.sol`
  - `omen/web/lib/mockContracts.ts`
  - `omen/web/lib/contracts.ts`
  - `omen/web/tests/contracts-robinhood-deploy.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mode mock simulator aktif secara default (`USE_MOCK_CONTRACT = true`) sehingga pengujian interaktif lokal dapat dijalankan seketika tanpa memerlukan wallet fisik atau faucet token.
