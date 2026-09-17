---
id: TICKET-107
title: Harmonize Bet & Position Indexing Payloads and Implement Market Claim Route
status: Done
priority: High
labels: [Frontend, Backend, BFF, Bets, Positions, Supabase]
---

# Deskripsi
Harmonisasi format kontrak data dan payload Backend-For-Frontend (BFF) antara Frontend (`usePlaceBet.ts`, `usePosition.ts`, `useClaim.ts`) dan Backend Route Handlers (`/api/bets/index`, `/api/markets/[id]/position`, `/api/markets/[id]/claim`). Memastikan route handler menerima format `snake_case` dan `camelCase` secara interoperable, serta mengimplementasikan endpoint rute klaim posisi (`/api/markets/[id]/claim`) untuk memperbarui status klaim taruhan di Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `web/app/api/bets/index/route.ts` mendukung parameter `contract_market_id`, `market_id`, dan `marketId`, serta normalisasi `side` dan `userAddress`.
- [x] `web/hooks/usePlaceBet.ts` mengirimkan payload yang selaras dan memeriksa status respon `res.ok`.
- [x] `web/app/api/markets/[id]/position/route.ts` mendukung parameter `wallet_address`, `userAddress`, `amount_eth`, `amount`, `tx_hash`, dan `txHash`.
- [x] `web/hooks/usePosition.ts` mengirimkan payload yang selaras ke rute posisi.
- [x] `web/app/api/markets/[id]/claim/route.ts` berhasil diimplementasikan untuk memvalidasi klaim dan memperbarui `claimed = true` di tabel `market_positions`.
- [x] `web/hooks/useClaim.ts` terhubung dan mengirimkan data klaim ke `/api/markets/[id]/claim`.
- [x] Seluruh unit test taruhan, posisi, dan klaim lulus tanpa regresi.

## Target Lingkup File (Affected Files)
- `web/app/api/bets/index/route.ts`
- `web/hooks/usePlaceBet.ts`
- `web/app/api/markets/[id]/position/route.ts`
- `web/hooks/usePosition.ts`
- `web/app/api/markets/[id]/claim/route.ts`
- `web/hooks/useClaim.ts`
- `web/tests/api-markets-claim.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyelaraskan destructuring dan validasi fleksibel pada `web/app/api/bets/index/route.ts`.
  2. Memperbarui `usePlaceBet.ts` dengan payload ganda dan verifikasi respon.
  3. Memperluas fleksibilitas parser parameter pada `web/app/api/markets/[id]/position/route.ts`.
  4. Menyelaraskan pengiriman payload pada `usePosition.ts`.
  5. Membuat file handler `web/app/api/markets/[id]/claim/route.ts` untuk memproses pemutakhiran `market_positions` saat user melakukan klaim payout on-chain.
  6. Memperbarui `useClaim.ts` untuk mengirimkan payload terstandarisasi.
  7. Menulis unit test suite `api-markets-claim.test.ts` (100% passed).
- **Ringkasan File Terpengaruh:**
  - `web/app/api/bets/index/route.ts`
  - `web/hooks/usePlaceBet.ts`
  - `web/app/api/markets/[id]/position/route.ts`
  - `web/hooks/usePosition.ts`
  - `web/app/api/markets/[id]/claim/route.ts`
  - `web/hooks/useClaim.ts`
  - `web/tests/api-markets-claim.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menerapkan prinsip defensive payload parsing pada BFF layer agar backward dan forward compatible.
