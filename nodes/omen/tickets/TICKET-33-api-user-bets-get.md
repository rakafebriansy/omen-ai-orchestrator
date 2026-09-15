---
id: TICKET-33
title: Pembuatan API Route Riwayat Taruhan
status: Todo
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
- [ ] Memfilter data riwayat taruhan berdasarkan alamat dompet pengguna.
- [ ] Menyatukan metadata status pasar untuk menentukan status menang/kalah.
- [ ] Unit test API route get user bets lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/bets/route.ts`
- `omen/web/tests/api-bets-get.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
