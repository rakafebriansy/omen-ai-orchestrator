---
id: TICKET-33
title: Pembuatan API Route Riwayat Taruhan
status: Done
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `GET /api/bets` di `omen/web/app/api/bets/route.ts` untuk menyajikan riwayat seluruh transaksi taruhan milik pengguna.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `GET`
- **Query Params:** `wallet_address=0x...`
- **Response:** Array riwayat taruhan memuat nama pasar, side (yes/no), amount, tx_hash, dan status claimed.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memfilter data riwayat taruhan berdasarkan alamat dompet pengguna.
- [x] Menyatukan metadata status pasar untuk menentukan status menang/kalah.
- [x] Unit test API route get user bets lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/bets/route.ts`
- `omen/web/tests/api-bets-get.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan Next.js serverless route handler `GET /api/bets` di `web/app/api/bets/route.ts` dengan validasi parameter `wallet_address` (format alamat EVM 42 karakter) dan normalisasi huruf kecil.
  2. Melakukan kueri riwayat taruhan pada tabel `bets` difilter berdasarkan alamat dompet pengguna dan terurut `created_at DESC`.
  3. Mengambil relasi metadata pasar dari tabel `markets` menggunakan set `market_id` unik untuk menyatukan nama pasar, batas waktu deadline, dan status pasar.
  4. Mengkalkulasi outcome dinamis taruhan (`active`, `won`, `lost`, `cancelled`) serta potensi payout proporsional pool atau pengembalian dana penuh pada pembatalan pasar.
  5. Membangun unit test suite Vitest di `web/tests/api-bets-get.test.ts` (6 skenario pengujian komprehensif) mencakup evaluasi multi-status pasar, user tanpa taruhan, penolakan missing/invalid wallet 400, error database 500, dan Zero-Comment Policy.
  6. Menjalankan pengujian otomatis Vitest (33 test files, 201 unit tests pass 100%) dan type checking `tsc --noEmit` (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/bets/route.ts`
  - `omen/web/tests/api-bets-get.test.ts`
  - `nodes/omen/tickets/TICKET-33-api-user-bets-get.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan teknik batch in-memory dictionary lookup untuk metadata `markets` untuk meminimalisir N+1 database queries.
  - Memastikan seluruh kode TypeScript mematuhi Zero-Comment Policy secara mutlak.
