---
id: TICKET-39
title: Integrasi Web3 Provider Wagmi di Layout Web
status: Done
priority: High
labels: [Frontend, Web3]
---

# Deskripsi
Mengintegrasikan WagmiConfig, QueryClientProvider, dan konfigurasi chain Arbitrum Sepolia ke dalam layout root `omen/web/app/providers.tsx` untuk mendukung interaksi dompet Phantom EVM.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Provider Web3
- Konfigurasi `createConfig` wagmi dengan transport `http()` ke RPC Arbitrum Sepolia.
- Inisialisasi `@tanstack/react-query` QueryClient.
- Komponen `Web3Providers` membungkus seluruh children pada root layout.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Wagmi provider membungkus aplikasi dan mengelola state koneksi dompet.
- [x] Dukungan mode EVM Phantom Wallet terdeteksi dengan baik.
- [x] Unit test wrapper Web3Providers lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/package.json`
- `omen/web/lib/wagmi.ts`
- `omen/web/app/providers.tsx`
- `omen/web/app/layout.tsx`
- `omen/web/tests/providers.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memasang dependensi Web3 inti `wagmi`, `viem`, dan `@tanstack/react-query` pada direktori `omen/web`.
  2. Mengonfigurasi `omen/web/lib/wagmi.ts` dengan chain Arbitrum Sepolia (Chain ID 421614), connector `injected({ target: "phantom" })` untuk mode Phantom EVM, fallback injected provider browser, HTTP RPC transport Arbitrum Sepolia, dan deklarasi TypeScript module augmentation.
  3. Membangun komponen client `Web3Providers` di `omen/web/app/providers.tsx` yang membungkus aplikasi menggunakan `WagmiProvider` dan `QueryClientProvider` dengan state queryClient stabil.
  4. Mengintegrasikan `Web3Providers` ke dalam `RootLayout` di `omen/web/app/layout.tsx` sehingga seluruh route halaman dan komponen dApp memiliki akses kontekstual Web3.
  5. Membuat test suite Vitest `omen/web/tests/providers.test.tsx` yang memvalidasi perenderan children di dalam context Wagmi/QueryClient, ketersediaan hook context, dan keakuratan rantai Arbitrum Sepolia.
  6. Menjalankan pengujian Vitest (130 test di 23 test file lolos 100%) dan verifikasi type check `npx tsc --noEmit` (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/package.json`
  - `omen/web/package-lock.json`
  - `omen/web/lib/wagmi.ts`
  - `omen/web/app/providers.tsx`
  - `omen/web/app/layout.tsx`
  - `omen/web/tests/providers.test.tsx`
  - `nodes/omen/tickets/TICKET-39-web3-provider-wagmi-integration.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengonfigurasi `injected({ target: "phantom" })` secara eksplisit untuk menjamin deteksi mulus saat pengguna berinteraksi menggunakan dompet Phantom pada mode rantai Ethereum/EVM.
