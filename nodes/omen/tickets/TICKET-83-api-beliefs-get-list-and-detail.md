---
id: TICKET-83
title: Pembuatan API Route Beliefs (GET /api/beliefs & GET /api/beliefs/[id])
status: Todo
priority: High
labels: [Backend, API, Supabase, Beliefs]
---

# Deskripsi
Tiket ini bertujuan membangun Next.js serverless route handlers untuk menyajikan katalog keyakinan sosial publik serta rincian spesifik satu belief.

Endpoint yang dibangun:
1. `GET /api/beliefs`:
   - Query params: `status` (`DETECTED`, `CONFIRMED`, `CLOSED`, `RESOLVED`, `ALL`), `author`, `sort` (`newest`, `highest_confidence`), `limit`, `offset`.
   - Mengambil data dari tabel `beliefs` dengan relasi ke `belief_sources` dan `markets`.
2. `GET /api/beliefs/[id]`:
   - Mengambil detail belief tunggal berdasarkan UUID dengan join lengkap ke tabel `belief_sources`, `markets`, `creator_confirmations`, dan `creator_profiles`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan `omen/web/app/api/beliefs/route.ts` untuk `GET /api/beliefs`.
- [ ] Mengimplementasikan `omen/web/app/api/beliefs/[id]/route.ts` untuk `GET /api/beliefs/[id]`.
- [ ] Mendukung filter query parameters, sorting, dan pagination yang efisien.
- [ ] Mengembalikan HTTP 404 jika ID belief tidak ditemukan dan HTTP 500 untuk error database.
- [ ] Menyusun unit test pada `omen/web/tests/api-beliefs-get.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/route.ts`
- `omen/web/app/api/beliefs/[id]/route.ts`
- `omen/web/tests/api-beliefs-get.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
