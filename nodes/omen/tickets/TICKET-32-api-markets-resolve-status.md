---
id: TICKET-32
title: Pembuatan API Route Pembaruan Status Pasar
status: Done
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
- [x] Memperbarui status pasar dan mencatat tautan bukti resolution_source.
- [x] Mencegah perubahan status jika pasar sudah pernah di-resolve sebelumnya.
- [x] Unit test API route resolve market lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/[id]/resolve/route.ts`
- `omen/web/tests/api-markets-resolve.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan Next.js App Router dynamic route handler `POST /api/markets/[id]/resolve` di `web/app/api/markets/[id]/resolve/route.ts` dengan asynchronous params unwrapping (`await context.params`).
  2. Mengimplementasikan proteksi otorisasi admin (`x-admin-key`, `Authorization: Bearer`, `x-admin-wallet`) dan validasi status target (`resolved_yes`, `resolved_no`, `cancelled`).
  3. Mendukung pencarian pasar ganda (Market UUID atau numeric `contract_market_id`), mencegah manipulasi berulang dengan menolak pasar non-aktif (HTTP 400 Bad Request anti-double resolve), serta memperbarui status dan `resolution_source`.
  4. Membangun unit test suite Vitest di `web/tests/api-markets-resolve.test.ts` (8 skenario pengujian komprehensif) mencakup resolusi yes/no/cancelled, lookup ID numeric, unauthorized 401, status invalid 400, not found 404, anti-double resolve 400, DB error 500, dan Zero-Comment Policy.
  5. Menjalankan pengujian otomatis Vitest (32 test files, 195 unit tests pass 100%) dan type checking `tsc --noEmit` (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/markets/[id]/resolve/route.ts`
  - `omen/web/tests/api-markets-resolve.test.ts`
  - `nodes/omen/tickets/TICKET-32-api-markets-resolve-status.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan conditional query regex UUID vs numeric ID agar frontend dapat memanggil endpoint baik dengan identifier internal Supabase maupun ID kontrak on-chain.
  - Memastikan seluruh kode TypeScript mematuhi Zero-Comment Policy secara mutlak.
