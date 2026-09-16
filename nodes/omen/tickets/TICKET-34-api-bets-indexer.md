---
id: TICKET-34
title: Pembuatan API Route Indexer Taruhan
status: Done
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
- [x] Mencegah duplikasi pencatatan tx_hash dengan constraint unik.
- [x] Menambahkan entri bonus poin partisipasi taruhan secara otomatis.
- [x] Unit test API route index bet lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/bets/index/route.ts`
- `omen/web/tests/api-bets-index.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan Next.js serverless route handler `POST /api/bets/index` di `web/app/api/bets/index/route.ts` dengan validasi ketat parameter `tx_hash`, `contract_market_id`, `wallet_address`, `side`, dan `amount`.
  2. Mengimplementasikan proteksi anti-duplikasi `tx_hash` dengan pemeriksaan record `bets` sebelumnya (HTTP 409 Conflict).
  3. Mengaitkan taruhan dengan pasar terkait via `contract_market_id`, menyimpan record ke tabel `bets`, dan mengupdate saldo total pool Yes / No pada tabel `markets`.
  4. Memberikan bonus reward aktivitas 50 poin ke `points_events` (`source: 'prediction_market'`) serta mengakumulasikan saldo `total_points` pengguna di tabel `users`.
  5. Membangun unit test suite Vitest di `web/tests/api-bets-index.test.ts` (8 skenario pengujian) mencakup pengindeksan posisi Yes dan No, pencegahan duplikasi tx_hash 409, validasi 400, not found 404, penanganan error 500, dan Zero-Comment Policy.
  6. Menjalankan pengujian otomatis Vitest (34 test files, 209 unit tests pass 100%) dan type checking `tsc --noEmit` (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/bets/index/route.ts`
  - `omen/web/tests/api-bets-index.test.ts`
  - `nodes/omen/tickets/TICKET-34-api-bets-indexer.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengkombinasikan atomic updates untuk tabel `bets`, `markets`, `users`, dan `points_events` agar seluruh pipeline Web3 event indexing tersinkronisasi secara konsisten dengan state database off-chain.
  - Memastikan seluruh kode TypeScript mematuhi Zero-Comment Policy secara mutlak.
