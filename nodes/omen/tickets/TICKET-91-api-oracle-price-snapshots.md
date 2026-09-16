---
id: TICKET-91
title: Pembuatan API Route Snapshot Harga Oracle Chainlink (POST /api/oracle/snapshot)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/app/api/oracle/snapshot/route.ts` untuk `POST /api/oracle/snapshot`.
- [ ] Menerapkan autentikasi admin/cron key yang ketat untuk mencegah manipulasi data snapshot.
- [ ] Membaca data harga resmi Chainlink feed dan menormalisasi format desimal mata uang (8/18 decimals).
- [ ] Menyimpan record ke tabel `oracle_snapshots` Supabase.
- [ ] Menyusun unit test pada `omen/web/tests/api-oracle-snapshot.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/oracle/snapshot/route.ts`
- `omen/web/lib/oracle/chainlink.ts`
- `omen/web/tests/api-oracle-snapshot.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
