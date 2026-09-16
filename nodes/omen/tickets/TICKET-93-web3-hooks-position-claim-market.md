---
id: TICKET-93
title: Pembuatan Web3 Wagmi Hooks (usePosition, useClaim, useMarket)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/hooks/usePosition.ts`, `omen/web/hooks/useClaim.ts`, dan `omen/web/hooks/useMarket.ts`.
- [ ] Menerapkan penanganan konversi nominal Wei/Ether yang aman dengan Viem `parseEther` dan `formatEther`.
- [ ] Melakukan sinkronisasi off-chain otomatis ke backend API saat transaksi berhasil.
- [ ] Menyediakan isolasi pengujian aman tanpa memerlukan koneksi ekstensi dompet nyata saat unit test dijalankan.
- [ ] Menyusun unit test pada `omen/web/tests/web3-hooks-v1.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/usePosition.ts`
- `omen/web/hooks/useClaim.ts`
- `omen/web/hooks/useMarket.ts`
- `omen/web/tests/web3-hooks-v1.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
