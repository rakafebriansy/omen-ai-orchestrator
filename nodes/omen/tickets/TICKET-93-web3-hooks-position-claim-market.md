---
id: TICKET-93
title: Pembuatan Web3 Wagmi Hooks (usePosition, useClaim, useMarket)
status: Done
priority: High
labels: [Frontend, Web3, Hooks, Wagmi]
---

# Deskripsi
Tiket ini menyediakan custom React hooks berbasis Wagmi v2 dan Viem untuk interaksi terintegrasi antara antarmuka pengguna OMEN dengan smart contract `OmenMarket.sol`:

1. `usePosition(marketAddress, side, amount)`:
   - Memanggil fungsi on-chain `depositAgree()` atau `depositDisagree()` dengan nilai ETH.
   - Mengelola state transaksi: `isPending`, `isConfirming`, `isSuccess`, `error`.
   - Mengindeks hasil transaksi secara otomatis ke endpoint off-chain `POST /api/markets/[id]/position` setelah receipt transaksi terkonfirmasi on-chain.
2. `useClaim(marketAddress)`:
   - Memanggil fungsi on-chain `claimPayout()`.
   - Mengelola loading state dan memicu refresh saldo/riwayat posisi pengguna saat klaim berhasil.
3. `useMarket(marketAddress)`:
   - Membaca state real-time dari kontrak on-chain: total agree pool, total disagree pool, status pasar, open time, dan close time.

> 🎨 **UI Style Preservation Note:**
> Integrasi hooks ke komponen UI (seperti `PositionPanel`, `ClaimPayoutButton`, dan `MarketDetailPanels`) **WAJIB MEMPERTAHANKAN** seluruh styling visual, indikator loading spinner, badge status, tombol bertema OpenZeppelin dark mode, dan alert dialog notifikasi transaksi.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/hooks/usePosition.ts`, `omen/web/hooks/useClaim.ts`, dan `omen/web/hooks/useMarket.ts`.
- [x] Menerapkan penanganan konversi nominal Wei/Ether yang aman dengan Viem `parseEther` dan `formatEther`.
- [x] Melakukan sinkronisasi off-chain otomatis ke backend API saat transaksi berhasil.
- [x] Menyediakan isolasi pengujian aman tanpa memerlukan koneksi ekstensi dompet nyata saat unit test dijalankan.
- [x] Menyusun unit test pada `omen/web/tests/web3-hooks-v1.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/usePosition.ts`
- `omen/web/hooks/useClaim.ts`
- `omen/web/hooks/useMarket.ts`
- `omen/web/tests/web3-hooks-v1.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Membuat `lib/contracts.ts` yang mendefinisikan ABI untuk `OmenMarket` dan `OmenFactory` serta `USE_MOCK_CONTRACT` toggle.
  2. Mengimplementasikan `usePosition.ts` dengan dukungan `depositAgree` dan `depositDisagree` berbasis Wagmi `useWriteContract` dan sinkronisasi off-chain `/api/markets/[id]/position`.
  3. Mengimplementasikan `useClaim.ts` untuk pemanggilan `claimPayout` on-chain dan sinkronisasi off-chain `/api/markets/[id]/claim`.
  4. Mengimplementasikan `useMarket.ts` untuk pembacaan pool summary `getMarketSummary` on-chain dan konversi Ether/Wei yang aman.
  5. Membuat suite unit test `tests/web3-hooks-v1.test.ts` dengan viem/wagmi hoisting mocks yang tervalidasi 100% lulus pada Vitest dan ESLint.
- **Ringkasan File Terpengaruh:**
  - `web/lib/contracts.ts`
  - `web/hooks/usePosition.ts`
  - `web/hooks/useClaim.ts`
  - `web/hooks/useMarket.ts`
  - `web/tests/web3-hooks-v1.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengeliminasi mutasi state di dalam `useEffect` pada `useMarket.ts` untuk memastikan kepatuhan penuh terhadap aturan rendering murni React 19 Compiler.
  - Mematuhi aturan Zero-Comment Policy pada seluruh source code dan test file.
