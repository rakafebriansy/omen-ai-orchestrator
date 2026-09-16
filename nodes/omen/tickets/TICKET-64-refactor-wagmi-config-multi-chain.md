---
id: TICKET-64
title: Refactor Wagmi Config & Web3 Providers untuk Ethereum Sepolia dan Robinhood Chain Testnet
status: Todo
priority: High
labels: [Frontend, Web3, Wagmi, Configuration]
---

# Deskripsi
Aplikasi saat ini dikonfigurasi untuk jaringan Arbitrum Sepolia (`421614`). Berdasarkan arsitektur OMEN V1 Social Belief Protocol, target testnet dialihkan ke **Ethereum Sepolia (`11155111`)** dan **Robinhood Chain Testnet (`46630`)**.

Tiket ini bertujuan merefaktor konfigurasi Wagmi dan Web3 Provider untuk mendukung dual testnet tersebut, memperbarui daftar wallet connector yang didukung (MetaMask, Rabby, Coinbase Wallet, WalletConnect, dan Robinhood Wallet), serta menyelaraskan dialog pemilihan jaringan.

> 🎨 **UI Style Preservation Note:**
> Seluruh komponen visual, modal dialog network switcher, tombol wallet, tipografi, warna badge, dan styling Tailwind yang sudah ada **WAJIB DIPERTAHANKAN**. Jangan merombak struktur styling atau mengubah tema visual OpenZeppelin dark mode yang sudah ada.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengubah konfigurasi chain utama pada `lib/wagmi.ts` dari `arbitrumSepolia` ke `sepolia` (Ethereum Sepolia, chain ID 11155111).
- [ ] Menambahkan definisi custom chain `robinhoodTestnet` (Chain ID 46630, RPC `https://rpc.testnet.chain.robinhood.com`, Native Currency `ETH`, Explorer `https://explorer.testnet.chain.robinhood.com`).
- [ ] Mengonfigurasi connector Wagmi untuk mendukung MetaMask (injected), Rabby, Coinbase Wallet, WalletConnect, dan generic EIP-6963 provider discovery.
- [ ] Memperbarui `NetworkSwitcherModal.tsx` agar menampilkan opsi switch antara Ethereum Sepolia dan Robinhood Chain Testnet dengan mempertahankan style UI dan animasi modal existing.
- [ ] Menjaga isolasi unit test pada `web/tests/providers.test.tsx` dan memastikan seluruh pengujian lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/lib/wagmi.ts`
- `omen/web/app/providers.tsx`
- `omen/web/components/NetworkSwitcherModal.tsx`
- `omen/web/tests/providers.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
