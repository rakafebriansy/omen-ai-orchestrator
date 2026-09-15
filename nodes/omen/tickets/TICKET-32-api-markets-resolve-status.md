---
id: TICKET-32
title: Pembuatan API Route Pembaruan Status Pasar
status: Todo
priority: Medium
labels: [Backend, API, Admin]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/markets/[id]/resolve` di `omen/web/app/api/markets/[id]/resolve/route.ts` untuk memperbarui status pasar di database setelah resolusi on-chain berhasil.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **URL Params:** `id` (Market UUID)
- **Request Body:** `{ status: 'resolved_yes' | 'resolved_no' | 'cancelled', resolution_source: string }`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memperbarui status pasar dan mencatat tautan bukti resolution_source.
- [ ] Mencegah perubahan status jika pasar sudah pernah di-resolve sebelumnya.
- [ ] Unit test API route resolve market lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/[id]/resolve/route.ts`
- `omen/web/tests/api-markets-resolve.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
