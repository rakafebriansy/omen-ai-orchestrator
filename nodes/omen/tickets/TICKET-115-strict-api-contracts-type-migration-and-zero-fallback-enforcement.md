---
id: TICKET-115
title: Strict API Contracts, Types Separation, and Zero-Fallback Enforcement
status: Done
priority: High
labels: [Backend, TypeScript, Refactor, ErrorHandling, Architecture]
---

# Deskripsi
Pemisahan seluruh TypeScript interface dan type definitions dari folder `web/app/api/` ke direktori khusus `web/types/` serta penegakan *zero-fallback policy* pada backend route handlers.

### Akar Masalah:
1. **Definisi Type Tersebar di Route Handlers:**
   - Interface database dan API response dideklarasikan secara *inline* di dalam file route (`web/app/api/markets/[id]/route.ts`), melanggar *separation of concerns*.
2. **Ketergantungan pada Fallback Artificial / Dummy Defaults:**
   - Adanya penggunaan operator `?? ""` atau fallback nilai statis yang menyamarkan data invalid/rusak di database, alih-alih melempar status error HTTP 400/500 yang jelas dan terstruktur.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Pindahkan seluruh interface dan tipe data API dari `web/app/api/` ke `web/types/api.ts` dan `web/types/index.ts`.
- [x] Hilangkan pemaksaan fallback `?? ""` pada data inti seperti `statement` dan `title`; lempar respons error HTTP 500 jika data esensial tidak valid di database.
- [x] Pertahankan integritas field database yang secara legal bernilai `null` (misalnya `author`, `authorHandle`, `source_url`, `creator_wallet`) tanpa menggantinya dengan empty string tiruan.
- [x] Pastikan seluruh test Vitest (77 test files, 395 unit tests) lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `web/types/api.ts`
- `web/types/index.ts`
- `web/app/api/markets/[id]/route.ts`
- `web/app/api/markets/route.ts`
- `web/app/api/beliefs/route.ts`
- `web/app/api/beliefs/[id]/route.ts`
- `web/tests/api-markets-get.test.ts`
- `web/tests/api-markets-v1-get.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Membuat file `web/types/api.ts` yang menampung interface kanonikal: `BeliefSourceRecord`, `CreatorConfirmationRecord`, `BeliefRecord`, `MarketResolutionRecord`, `MarketRecord`, `FormattedMarketDetail`, dan `MarketDetailApiResponse`.
  2. Mengekspor kembali seluruh tipe dari `web/types/index.ts`.
  3. Mengupdate `web/app/api/markets/[id]/route.ts` untuk mengimpor dari `@/types/api` dan menegakkan validasi `statement` tanpa fallback dummy.
  4. Menyelaraskan seluruh unit test mock dan assertions.
  5. Memastikan 0 komentar kode, 0 error TypeScript, dan 0 warning lint.
- **Ringkasan File Terpengaruh:**
  - `web/types/api.ts`
  - `web/types/index.ts`
  - `web/app/api/markets/[id]/route.ts`
  - `web/app/api/markets/route.ts`
  - `web/tests/api-markets-get.test.ts`
  - `web/tests/api-markets-v1-get.test.ts`
- **Catatan dan Keputusan Arsitektural:**
  - Menerapkan arsitektur tipe tersentralisasi untuk mempermudah pemeliharaan jangka panjang dan sinkronisasi antara backend route handlers dan frontend components.
