---
id: TICKET-31
title: Pembuatan API Route Simpan Pasar Baru
status: Todo
priority: Medium
labels: [Backend, API, Admin]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/markets` di `omen/web/app/api/markets/route.ts` khusus admin untuk menyimpan metadata pasar baru ke basis data Supabase pasca pembuatan on-chain.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **Request Body:** `{ contract_market_id, title, description, deadline, category }`
- **Proteksi:** Otorisasi admin via secret key / wallet signature.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyimpan metadata pasar baru dengan contract_market_id unik.
- [ ] Memvalidasi otorisasi admin dan menolak permintaan tanpa wewenang.
- [ ] Unit test API route create market lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`
- `omen/web/tests/api-markets-create.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
