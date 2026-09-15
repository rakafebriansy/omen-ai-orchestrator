---
id: TICKET-39
title: Integrasi Web3 Provider Wagmi di Layout Web
status: Todo
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
- [ ] Wagmi provider membungkus aplikasi dan mengelola state koneksi dompet.
- [ ] Dukungan mode EVM Phantom Wallet terdeteksi dengan baik.
- [ ] Unit test wrapper Web3Providers lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/providers.tsx`
- `omen/web/lib/wagmi.ts`
- `omen/web/tests/providers.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
