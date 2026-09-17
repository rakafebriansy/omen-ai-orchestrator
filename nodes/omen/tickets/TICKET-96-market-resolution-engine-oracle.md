---
id: TICKET-96
title: Implementasi Market Resolution Engine Berbasis Data Oracle Otomatis
status: Done
priority: High
labels: [Backend, Oracle, Resolution, Engine]
---

# Deskripsi
Tiket ini membangun mesin penyelesaian pasar otomatis (*Market Resolution Engine*) di sisi server untuk menutup dan menyelesaikan pasar keyakinan yang telah melewati masa berlakunya (*deadline expiration*).

Alur kerja engine:
1. Menemukan seluruh pasar dengan status `OPEN` yang telah melewati `close_time` (`now >= close_time`).
2. Mengubah status pasar menjadi `CLOSED` (menghentikan penerimaan setoran posisi baru).
3. Mengambil snapshot harga akhir (*END snapshot*) dari Chainlink Oracle feed via `POST /api/oracle/snapshot`.
4. Mengevaluasi kriteria resolusi menggunakan modul `chainlink.ts` untuk menentukan pemenang (`AGREE_WON`, `DISAGREE_WON`, atau `VOID`).
5. Memanggil fungsi on-chain `OmenMarket.resolveMarket(outcome)` menggunakan admin resolver private key.
6. Memperbarui database Supabase via `POST /api/markets/[id]/resolve`.
7. Menyediakan fail-safe fallback: Jika oracle mengalami downtime atau malfungsi data feed, pasar ditandai sebagai `VOID` agar seluruh partisipan dapat melakukan penarikan refund penuh 100%.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/lib/market/resolution-engine.ts`.
- [x] Menyediakan fungsi `processPendingResolutions()` yang dapat dipicu oleh cron job scheduler atau webhook.
- [x] Menangani eksekusi on-chain `resolveMarket` dengan manajemen gas fee dan konfirmasi receipt.
- [x] Mengimplementasikan fail-safe fallback `voidMarket` jika data oracle tidak tersedia atau terjadi anomali harga ekstrem.
- [x] Menyusun unit test pada `omen/web/tests/resolution-engine.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/lib/market/resolution-engine.ts`
- `omen/web/tests/resolution-engine.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/resolution-engine.test.ts` untuk pengujian kepatuhan Zero-Comment Policy, deteksi batch pasar kadaluarsa (`processPendingResolutions`), evaluasi harga oracle Chainlink, eksekusi on-chain, dan mekanisme fail-safe fallback otomatis ke status `VOID` saat oracle mengalami timeout atau error.
  2. Mengembangkan modul mesin resolusi otomatis `omen/web/lib/market/resolution-engine.ts` dengan fungsi `processPendingResolutions` dan `resolveSingleMarket`.
  3. Mengintegrasikan penulisan rekaman harga akhir ke `oracle_snapshots`, eksekusi fungsi on-chain `OmenMarket.resolveMarket(outcome)`, serta sinkronisasi status ke tabel `markets`, `beliefs`, `market_resolutions`, `market_settlements`, dan `creator_profiles`.
  4. Menjalankan pengujian vitest (320 tests pass di 56 test files), typecheck `tsc`, dan linter ESLint (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/market/resolution-engine.ts`
  - `omen/web/tests/resolution-engine.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menerapkan isolasi kegagalan per-pasar di dalam batch loop sehingga kegagalan satu pasar (misal RPC error) tidak menggagalkan resolusi pasar lainnya. Perlindungan fail-safe fallback memastikan tidak ada dana pengguna yang terkunci selamanya ketika oracle gagal.
