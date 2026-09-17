---
id: TICKET-91
title: Pembuatan API Route Snapshot Harga Oracle Chainlink (POST /api/oracle/snapshot)
status: Done
priority: Medium
labels: [Backend, API, Oracle, Chainlink]
---

# Deskripsi
Pasar keyakinan berbasis oracle (misal: "SOL akan mengungguli ETH dalam 7 hari" atau "ETH akan melewati $4000 pada tanggal X") memerlukan titik referensi harga awal (*START price*) dan harga akhir (*END price*) yang dicatat secara deterministik dari Chainlink Data Feeds.

Endpoint `POST /api/oracle/snapshot` bertugas:
1. Menerima request terproteksi (via `x-admin-key` atau cron trigger token).
2. Membaca harga terkini dari kontrak Chainlink Aggregator V3 interface on-chain (atau cache price feed).
3. Menyimpan snapshot harga ke tabel `oracle_snapshots` dengan atribut: `market_id`, `asset_symbol`, `price_usd`, `snapshot_type` (`START` | `END` | `DISPLAY`), `source` (`chainlink`), dan `recorded_at`.
4. Mengembalikan konfirmasi snapshot tersimpan untuk proses pembukaan atau penutupan pasar.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/app/api/oracle/snapshot/route.ts` untuk `POST /api/oracle/snapshot`.
- [x] Menerapkan autentikasi admin/cron key yang ketat untuk mencegah manipulasi data snapshot.
- [x] Membaca data harga resmi Chainlink feed dan menormalisasi format desimal mata uang (8/18 decimals).
- [x] Menyimpan record ke tabel `oracle_snapshots` Supabase.
- [x] Menyusun unit test pada `omen/web/tests/api-oracle-snapshot.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/oracle/snapshot/route.ts`
- `omen/web/lib/oracle/chainlink.ts`
- `omen/web/tests/api-oracle-snapshot.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/api-oracle-snapshot.test.ts` yang mencakup validasi Zero-Comment Policy, normalisasi desimal Chainlink (8 decimals), proteksi otentikasi header `x-admin-key`/bearer (HTTP 401), validasi parameter required `asset` (HTTP 400), penyimpanan snapshot harga statis dan dinamis on-chain via feed reader.
  2. Mengembangkan modul `omen/web/lib/oracle/chainlink.ts` dengan ABI Aggregator V3, konfigurasi alamat data feed resmi di Sepolia dan Arbitrum Sepolia, utilitas normalisasi harga `normalizeChainlinkPrice`, dan fungsi pembaca feed on-chain `fetchChainlinkPrice`.
  3. Mengembangkan route handler `POST /api/oracle/snapshot` pada `omen/web/app/api/oracle/snapshot/route.ts` yang mengeksekusi verifikasi admin key, fetch harga on-chain jika harga tidak diinput manual, dan penyimpanan ke tabel `oracle_snapshots` Supabase.
  4. Menjalankan pengujian vitest, linter ESLint, dan typechecking tsc (100% pass, 0 lint error, 0 comment).
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/oracle/chainlink.ts`
  - `omen/web/app/api/oracle/snapshot/route.ts`
  - `omen/web/tests/api-oracle-snapshot.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan interface standar Chainlink Aggregator V3 (`latestRoundData`) yang mengembalikan `int256 answer` dengan pembagian skala 8 desimal untuk pairs aset kripto / USD.
