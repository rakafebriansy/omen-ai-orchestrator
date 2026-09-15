---
id: TICKET-28
title: Pembuatan API Route Verifikasi Quest
status: Todo
priority: Medium
labels: [Backend, API, Gamification]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/quests/[id]/complete` di `omen/web/app/api/quests/[id]/complete/route.ts` untuk memverifikasi penyelesaian misi dan memberikan reward poin.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **URL Params:** `id` (Quest UUID)
- **Request Body:** `{ wallet_address: string }`
- **Validasi:** Mencegah klaim ganda dengan mengecek keberadaan entri di `points_events`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memvalidasi quest aktif dan mencegah eksploitasi perolehan poin ganda.
- [ ] Menambah total_points pengguna dan mencatat ke points_events.
- [ ] Unit test API route quest completion lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/quests/[id]/complete/route.ts`
- `omen/web/tests/api-quest-complete.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
