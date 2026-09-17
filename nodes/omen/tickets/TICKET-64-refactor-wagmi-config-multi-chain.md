---
id: TICKET-64
title: Refactor Wagmi Config & Web3 Providers untuk Ethereum Sepolia dan Robinhood Chain Testnet
status: Done
priority: High
labels: [Frontend, Web3, Wagmi, Configuration]
---

# Deskripsi
Aplikasi saat ini dikonfigurasi untuk jaringan Arbitrum Sepolia (`421614`). Berdasarkan arsitektur OMEN V1 Social Belief Protocol, target testnet dialihkan ke **Ethereum Sepolia (`11155111`)** dan **Robinhood Chain Testnet (`46630`)**.

Tiket ini bertujuan merefaktor konfigurasi Wagmi dan Web3 Provider untuk mendukung dual testnet tersebut, memperbarui daftar wallet connector yang didukung (MetaMask, Rabby, Coinbase Wallet, WalletConnect, dan Robinhood Wallet), serta menyelaraskan dialog pemilihan jaringan.

> 🎨 **UI Style Preservation Note:**
> Seluruh komponen visual, modal dialog network switcher, tombol wallet, tipografi, warna badge, dan styling Tailwind yang sudah ada **WAJIB DIPERTAHANKAN**. Jangan merombak struktur styling atau mengubah tema visual OpenZeppelin dark mode yang sudah ada.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengubah konfigurasi chain utama pada `lib/wagmi.ts` dari `arbitrumSepolia` ke `sepolia` (Ethereum Sepolia, chain ID 11155111).
- [x] Menambahkan definisi custom chain `robinhoodTestnet` (Chain ID 46630, RPC `https://rpc.testnet.chain.robinhood.com`, Native Currency `ETH`, Explorer `https://explorer.testnet.chain.robinhood.com`).
- [x] Mengonfigurasi connector Wagmi untuk mendukung MetaMask (injected), Rabby, Coinbase Wallet, WalletConnect, dan generic EIP-6963 provider discovery.
- [x] Memperbarui `NetworkSwitcherModal.tsx` agar menampilkan opsi switch antara Ethereum Sepolia dan Robinhood Chain Testnet dengan mempertahankan style UI dan animasi modal existing.
- [x] Menjaga isolasi unit test pada `web/tests/providers.test.tsx` dan memastikan seluruh pengujian lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/lib/wagmi.ts`
- `omen/web/app/providers.tsx`
- `omen/web/components/NetworkSwitcherModal.tsx`
- `omen/web/tests/providers.test.tsx`
- `omen/web/tests/network-switcher.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memperbarui test suite `web/tests/providers.test.tsx` dan `web/tests/network-switcher.test.tsx` dengan assertions untuk Ethereum Sepolia (11155111) dan Robinhood Chain Testnet (46630).
  2. Mengonfigurasi custom chain `robinhoodTestnet` via `defineChain` (Viem) dan mendaftarkan `sepolia` serta `robinhoodTestnet` pada `web/lib/wagmi.ts`.
  3. Menambahkan dukungan multi-connector (MetaMask, Phantom, Rabby, Coinbase Wallet, dan generic injected) serta fallback RPC transports pada `web/lib/wagmi.ts`.
  4. Merefaktor `web/components/NetworkSwitcherModal.tsx` agar mendukung pemilihan interaktif antara Ethereum Sepolia dan Robinhood Chain Testnet dengan preservasi tema OpenZeppelin dark mode dan aksesibilitas ARIA.
  5. Memvalidasi 100% kelulusan unit test (249 tests passing) dan pemeriksaan linter bersih tanpa pelanggaran Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/wagmi.ts`
  - `omen/web/components/NetworkSwitcherModal.tsx`
  - `omen/web/tests/providers.test.tsx`
  - `omen/web/tests/network-switcher.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan `defineChain` dari `viem` untuk `robinhoodTestnet` (Chain ID 46630) agar memiliki full type safety pada Wagmi configuration.
  - Mempertahankan backward compatibility untuk prop `targetChainId` dan `targetNetworkName` pada `NetworkSwitcherModal.tsx` sembari menyediakan daftar pilihan jaringan aktif.
