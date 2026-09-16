---
id: TICKET-28
title: Pembuatan API Route Verifikasi Quest
status: Done
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
- [x] Memvalidasi quest aktif dan mencegah eksploitasi perolehan poin ganda.
- [x] Menambah total_points pengguna dan mencatat ke points_events.
- [x] Unit test API route quest completion lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/quests/[id]/complete/route.ts`
- `omen/web/tests/api-quest-complete.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan serverless Next.js API route handler `POST /api/quests/[id]/complete` di `omen/web/app/api/quests/[id]/complete/route.ts`.
  2. Mengimplementasikan ekstraksi parameter asynchronous `await context.params` sesuai kaidah Next.js 15/16 App Router.
  3. Memvalidasi keberadaan dan keaktifan misi (`is_active: true`), keberadaan profil pengguna terdaftar, serta proteksi anti-double claim dengan memverifikasi ketiadaan riwayat pada tabel `points_events` untuk pasangan dompet dan quest terkait.
  4. Melakukan penambahan poin reward ke `total_points` pengguna pada tabel `users` dan menginsert entri transaksi audit log ke `points_events` (`source: 'quest'`).
  5. Menulis unit test komprehensif di `omen/web/tests/api-quest-complete.test.ts` (8 skenario uji: validasi payload, 404 quest tidak ditemukan, 400 quest non-aktif, 404 user tidak ditemukan, 400 proteksi double claim, 200 verifikasi sukses, dan Zero-Comment Policy).
  6. Memvalidasi seluruh test suite Vitest `npm run test` (28 file, 167 test lolos 100%) dan type check `npx tsc --noEmit` lolos tanpa error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/quests/[id]/complete/route.ts` (Created)
  - `omen/web/tests/api-quest-complete.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-28-api-quest-completion-verification.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengisolasi pencatatan event gamifikasi dengan menyertakan `quest_id` Foreign Key eksplisit agar integritas data antara reward poin dan entitas quest tetap terjaga secara konsisten.
