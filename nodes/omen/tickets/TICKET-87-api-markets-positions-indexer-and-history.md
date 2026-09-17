---
id: TICKET-87
title: Pembuatan API Route Positions Indexer & History (POST /api/markets/[id]/position & GET /api/positions)
status: Done
priority: High
labels: [Backend, API, Indexer, Positions]
---

# Deskripsi
Tiket ini membangun sistem pencatatan dan pelacakan posisi keyakinan pengguna:
1. `POST /api/markets/[id]/position`:
   - Mengindeks event setoran on-chain (`PositionTaken`) ke tabel `market_positions`.
   - Memvalidasi parameter: `wallet_address`, `side` (`AGREE` | `DISAGREE`), `amount_eth`, `tx_hash`.
   - Memperbarui akumulator pool pasar pada tabel `markets` (`agree_pool`, `disagree_pool`, `agree_count`, `disagree_count`).
   - Mencatat log event ke tabel `market_events`.
   - Menggunakan proteksi idempotency berbasis `tx_hash` unik untuk mencegah duplikasi (HTTP 409 Conflict).
2. `GET /api/positions`:
   - Mengambil seluruh riwayat posisi pengguna yang terhubung (`?wallet=0x...`).
   - Mengkalkulasi status dinamis posisi (`OPEN`, `WON`, `LOST`, `CLAIMED`, `REFUNDED`) dan estimasi payout hasil kalkulasi proporsional.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/app/api/markets/[id]/position/route.ts` untuk pengindeksan posisi on-chain.
- [x] Mengimplementasikan `omen/web/app/api/positions/route.ts` untuk riwayat portofolio pengguna.
- [x] Mencegah duplikasi indeks transaksi dengan constraint unik pada `tx_hash`.
- [x] Memperbarui nilai pool dan jumlah partisipan pasar secara atomik/tervalidasi.
- [x] Menyusun unit test pada `omen/web/tests/api-positions.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/[id]/position/route.ts`
- `omen/web/app/api/positions/route.ts`
- `omen/web/tests/api-positions.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test TDD di `omen/web/tests/api-positions.test.ts` untuk memvalidasi indexing posisi, proteksi idempotensi `tx_hash` (HTTP 409), pencatatan event log `PositionTaken`, pembaruan akumulator pool pasar, serta kalkulasi status portofolio dinamis pengguna (`OPEN`, `WON`, `LOST`, `CLAIMED`, `REFUNDED`) dan estimasi payout.
  2. Mengimplementasikan handler endpoint `POST /api/markets/[id]/position/route.ts` dengan validasi parameter, pencegahan duplikasi `tx_hash`, dan pembaruan pool pasar.
  3. Mengimplementasikan handler endpoint `GET /api/positions/route.ts` untuk query portofolio posisi pengguna berdasarkan alamat wallet beserta kalkulasi status dan estimasi hadiah.
  4. Menjalankan pengujian Vitest: seluruh 6 test `api-positions.test.ts` dan 277 total test aplikasi lulus 100%.
  5. Memvalidasi type checking `tsc --noEmit` dan linter `eslint` dengan 0 error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/markets/[id]/position/route.ts` (API route pengindeksan posisi onchain & event logger)
  - `omen/web/app/api/positions/route.ts` (API route riwayat portofolio dan kalkulasi payout posisi pengguna)
  - `omen/web/tests/api-positions.test.ts` (Unit test suite untuk positions API)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Idempotensi transaksi ditegakkan pada layer database dan endpoint API untuk menjamin saldo pool tidak mengalami inflasi data jika indexer/client memicu retry.
  - Zero-Comment Policy dipatuhi secara ketat di seluruh kode.
