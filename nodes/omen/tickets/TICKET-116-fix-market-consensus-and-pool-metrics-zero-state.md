---
id: TICKET-116
title: Fix Market Consensus and Pool Metrics Zero-State and Eliminate Aliased Duplicate Payload Properties
status: Done
priority: High
labels: [Frontend, Backend, Calculation, Bug, UI]
---

# Deskripsi
Perbaikan bug kalkulasi dan tampilan persentase metrik Consensus (People) dan Money (Pool) pada kartu pasar belief (`BeliefMarketCard.tsx`), halaman discovery feed (`/markets`), teaser landing page (`TrendingMarketsTeaser.tsx`), serta halaman detail pasar (`/market/[id]`).

### Akar Masalah:
1. **Fallback Dummy Participants:**
   - Di `web/app/markets/page.tsx` dan `web/components/landing/TrendingMarketsTeaser.tsx`, pemetaan respons API menggunakan nilai tiruan `10` dan `5`:
     ```typescript
     agreeParticipants: Number(m.agreeParticipants ?? m.agree_participants ?? 10)
     disagreeParticipants: Number(m.disagreeParticipants ?? m.disagree_participants ?? 5)
     ```
   - Akibatnya, market dengan 0 partisipan keliru menampilkan `67% AGREE / 33% DISAGREE`.
2. **Fallback Persentase 50% pada Pool 0 ETH:**
   - Di `web/components/BeliefMarketCard.tsx` dan `MarketDetailPanels.tsx`, kalkulasi persentase jatuh ke `50%` saat `totalPool === 0` atau `totalParticipants === 0`, sehingga bar terisi 50%/50% padahal pool masih 0 ETH.
3. **Ketiadaan Agregasi Posisi di `GET /api/markets`:**
   - Endpoint `GET /api/markets` tidak meng-query relasi `market_positions`, sehingga field jumlah partisipan tidak terhitung secara akurat.
4. **Duplikasi Field Payload (Redundant Aliases):**
   - Munculnya properti ganda pada respons JSON (misal `agree_participants` bersamaan dengan `agreeParticipants`).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Perbaiki logika 0-state pada `BeliefMarketCard.tsx` dan `MarketDetailPanels.tsx`: jika `totalPool === 0` atau `totalParticipants === 0`, set persentase ke `0%` dan lebar progress bar ke `0%`.
- [x] Hapus nilai fallback dummy `10` dan `5` dari `web/app/markets/page.tsx` dan `TrendingMarketsTeaser.tsx`; gunakan default `0`.
- [x] Query tabel relasi `market_positions` di `web/app/api/markets/route.ts` dan `web/app/api/markets/[id]/route.ts` untuk menghitung `agree_participants` dan `disagree_participants` aktual.
- [x] Hapus duplikasi properti camelCase/snake_case di level API JSON response dan standarkan ke format snake_case kanonikal.
- [x] Pastikan seluruh test Vitest (77 test suites, 395 unit tests) lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `web/components/BeliefMarketCard.tsx`
- `web/components/MarketDetailPanels.tsx`
- `web/app/markets/page.tsx`
- `web/components/landing/TrendingMarketsTeaser.tsx`
- `web/app/market/[id]/page.tsx`
- `web/app/api/markets/route.ts`
- `web/app/api/markets/[id]/route.ts`
- `web/types/api.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Memperbarui `BeliefMarketCard.tsx` agar mengembalikan persentase `0%` saat total adalah 0.
  2. Memperbarui `web/app/api/markets/route.ts` untuk menyertakan `market_positions` dan menghitung jumlah partisipan AGREE/DISAGREE secara dinamis.
  3. Menghapus properti duplikat `agreeParticipants` dan `disagreeParticipants` dari API response payload.
  4. Menyelaraskan komponen halaman discovery dan teaser landing page dengan default `0`.
  5. Menjalankan verifikasi penuh `npm test` dan `git diff` untuk memastikan kepatuhan Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `web/components/BeliefMarketCard.tsx`
  - `web/components/MarketDetailPanels.tsx`
  - `web/app/markets/page.tsx`
  - `web/components/landing/TrendingMarketsTeaser.tsx`
  - `web/app/market/[id]/page.tsx`
  - `web/app/api/markets/route.ts`
  - `web/app/api/markets/[id]/route.ts`
  - `web/types/api.ts`
- **Catatan dan Keputusan Arsitektural:**
  - Mengadopsi prinsip single canonical naming: snake_case di layer REST API database, dan ditransformasikan secara eksplisit menjadi camelCase hanya di layer view components tanpa redundansi alias ganda.
