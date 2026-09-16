---
id: TICKET-43
title: Integrasi Transaksi Admin Resolusi Pasar
status: Done
priority: Medium
labels: [Frontend, Web3, Admin]
---

# Deskripsi
Menghubungkan antarmuka `AdminMarketResolutionTable` ke fungsi `resolveMarket` smart contract on-chain dan memperbarui status pasar di Supabase via `POST /api/markets/[id]/resolve`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Alur Integrasi Admin Resolve
1. Admin memilih hasil Yes atau No dan menandatangani transaksi `resolveMarket(marketId, result)`.
2. Setelah transaksi on-chain sukses, memanggil API `POST /api/markets/[id]/resolve` untuk memperbarui status pasar di database.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Status pasar di smart contract terkunci permanen pada hasil pemenang.
- [x] Status pasar di database Supabase terbarui ke resolved_yes atau resolved_no.
- [x] Tabel resolusi admin memperbarui daftar pasar yang tersisa.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useAdminResolveMarket.ts`
- `omen/web/components/AdminMarketResolutionTable.tsx`
- `omen/web/tests/admin-resolve-market.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan custom hook `useAdminResolveMarket` di `omen/web/hooks/useAdminResolveMarket.ts` memanfaatkan `useWriteContract`, `useWaitForTransactionReceipt`, `useAccount`, dan context guard `WagmiContext`.
  2. Mendukung eksekusi transaksi on-chain `resolveMarket(marketId, result)` untuk outcome YES dan NO, serta `cancelMarket(marketId)` untuk pembatalan dan refund 100%.
  3. Memicu sinkronisasi status ke backend Supabase melalui `POST /api/markets/${marketId}/resolve` dengan parameter status terpetakan (`resolved_yes`, `resolved_no`, `cancelled`).
  4. Mengintegrasikan `useAdminResolveMarket` ke dalam `AdminMarketResolutionTable.tsx` pada `handleConfirmResolution`, mempertahankan fungsionalitas callback `onResolveMarket`.
  5. Menulis unit test suite di `omen/web/tests/admin-resolve-market.test.ts` (4/4 tests pass) dan memverifikasi seluruh test suite (27 test files / 143 tests di `omen/web` lulus 100%, 19 unit tests di `omen/contracts` lulus 100%) dan `tsc --noEmit` 0 galat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/hooks/useAdminResolveMarket.ts`
  - `omen/web/components/AdminMarketResolutionTable.tsx`
  - `omen/web/tests/admin-resolve-market.test.ts`
  - `nodes/omen/tickets/TICKET-43-admin-resolve-market-wiring.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengimplementasikan parsing ID dinamis yang mengekstrak digit numerik secara aman untuk konversi ke `BigInt(numericMarketId)`, kompatibel dengan format mock maupun contract market ID asli.
  - Memastikan seluruh kode TypeScript mematuhi aturan Zero-Comment Policy secara mutlak.
