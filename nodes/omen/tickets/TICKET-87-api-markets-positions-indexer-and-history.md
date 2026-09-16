---
id: TICKET-87
title: Pembuatan API Route Positions Indexer & History (POST /api/markets/[id]/position & GET /api/positions)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/app/api/markets/[id]/position/route.ts` untuk pengindeksan posisi on-chain.
- [ ] Mengimplementasikan `omen/web/app/api/positions/route.ts` untuk riwayat portofolio pengguna.
- [ ] Mencegah duplikasi indeks transaksi dengan constraint unik pada `tx_hash`.
- [ ] Memperbarui nilai pool dan jumlah partisipan pasar secara atomik/tervalidasi.
- [ ] Menyusun unit test pada `omen/web/tests/api-positions.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/[id]/position/route.ts`
- `omen/web/app/api/positions/route.ts`
- `omen/web/tests/api-positions.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
