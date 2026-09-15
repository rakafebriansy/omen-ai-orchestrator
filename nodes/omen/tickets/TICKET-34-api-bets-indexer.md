---
id: TICKET-34
title: Pembuatan API Route Indexer Taruhan
status: Todo
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/bets/index` di `omen/web/app/api/bets/index/route.ts` untuk mencatat event transaksi taruhan on-chain dan memberikan reward poin partisipasi.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **Request Body:** `{ tx_hash, contract_market_id, wallet_address, side, amount }`
- **Logika:**
  1. Menyimpan record taruhan baru ke tabel `bets`.
  2. Memberikan bonus poin aktivitas ke `points_events` dan mengupdate `users.total_points`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mencegah duplikasi pencatatan tx_hash dengan constraint unik.
- [ ] Menambahkan entri bonus poin partisipasi taruhan secara otomatis.
- [ ] Unit test API route index bet lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/bets/index/route.ts`
- `omen/web/tests/api-bets-index.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
