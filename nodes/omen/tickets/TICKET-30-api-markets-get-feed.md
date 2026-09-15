---
id: TICKET-30
title: Pembuatan API Route Katalog Pasar
status: Todo
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `GET /api/markets` di `omen/web/app/api/markets/route.ts` untuk menyajikan katalog pasar prediksi dengan filter status dan kategori.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `GET`
- **Query Params:** `status` (active, resolved, all), `category` (crypto, meme, all), `sort` (highest_pool, newest)
- **Response:** Array data pasar prediksi beserta rincian pool Yes dan No.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mendukung filter status pasar dan kategori secara dinamis.
- [ ] Mengembalikan kalkulasi total pool dan batas waktu deadline.
- [ ] Unit test API route get markets lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`
- `omen/web/tests/api-markets-get.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
