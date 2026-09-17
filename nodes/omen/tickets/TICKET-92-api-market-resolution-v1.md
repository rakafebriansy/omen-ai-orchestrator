---
id: TICKET-92
title: Refactor API Route Resolusi Pasar V1 (POST /api/markets/[id]/resolve)
status: Done
priority: High
labels: [Backend, API, Resolution, Settlement]
---

# Deskripsi
Endpoint resolusi pasar (`POST /api/markets/[id]/resolve`) perlu diselaraskan dengan arsitektur V1:
1. **Outcome Model Baru:** Mendukung `AGREE_WON`, `DISAGREE_WON`, dan `VOID` (menggantikan enum lama `resolved_yes`, `resolved_no`, `cancelled`).
2. **Oracle Verification:** Memvalidasi perbandingan harga `START` vs `END` dari tabel `oracle_snapshots` sesuai kriteria (`PRICE_ABOVE`, `PRICE_BELOW`, `RELATIVE_PERFORMANCE`).
3. **Pencatatan Resolusi & Settlement:** Menyimpan entri ke `market_resolutions` dan menginisialisasi alokasi pool di `market_settlements`.
4. **Pembaruan Status & Reputasi:**
   - Memperbarui `markets.status` menjadi `RESOLVED` (atau `VOID`).
   - Memperbarui `beliefs.status` menjadi `RESOLVED`.
   - Menghitung akurasi kreator pada `creator_profiles` (menambah `resolved_beliefs` dan `correct_beliefs` jika prediksi kreator terbukti akurat).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memperbarui `omen/web/app/api/markets/[id]/resolve/route.ts` dengan dukungan outcome V1.
- [x] Menerapkan otorisasi admin/resolver key yang ketat.
- [x] Melakukan mutasi terkoordinasi pada tabel `markets`, `beliefs`, `market_resolutions`, `market_settlements`, dan `creator_profiles`.
- [x] Mencegah resolusi ulang pada pasar yang sudah berstatus `RESOLVED`, `SETTLED`, atau `VOID` (HTTP 400).
- [x] Menyusun unit test pada `omen/web/tests/api-markets-v1-resolve.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/[id]/resolve/route.ts`
- `omen/web/lib/market/resolution-helper.ts`
- `omen/web/tests/api-markets-v1-resolve.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/api-markets-v1-resolve.test.ts` untuk pengujian normalisasi outcome V1/legacy, kalkulasi settlement pool, proteksi otentikasi admin, penolakan resolusi ganda (HTTP 400), dan update terkoordinasi pada seluruh tabel terkait.
  2. Mengembangkan modul helper `omen/web/lib/market/resolution-helper.ts` dengan fungsi `normalizeOutcome`, `calculateSettlementPool` (termasuk 0 fee untuk VOID refund), dan `evaluateOracleCondition`.
  3. Memperbarui handler `POST /api/markets/[id]/resolve` pada `omen/web/app/api/markets/[id]/resolve/route.ts` dengan mutasi atomik pada `markets`, `beliefs`, `market_resolutions`, `market_settlements`, dan `creator_profiles`.
  4. Menjalankan pengujian vitest (313 tests pass di 54 test files), typecheck `tsc`, dan linter ESLint (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/market/resolution-helper.ts`
  - `omen/web/app/api/markets/[id]/resolve/route.ts`
  - `omen/web/tests/api-markets-v1-resolve.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengadopsi arsitektur resolusi hybrid yang mempertahankan kompatibilitas payload legacy (`resolved_yes`, `resolved_no`, `cancelled`) sekaligus mendukung standar V1 (`AGREE`, `DISAGREE`, `VOID`) dengan kalkulasi otomatis pemotongan biaya protokol 2% saat settlement.
