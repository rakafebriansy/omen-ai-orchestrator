---
id: TICKET-26
title: Pembuatan API Route Daily Check-in Streak
status: Done
priority: Medium
labels: [Backend, API, Gamification]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/checkin` di `omen/web/app/api/checkin/route.ts` untuk memvalidasi batas waktu 24 jam check-in, mengelola streak counter, dan mengalokasikan reward poin ke audit log.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **Request Body:** `{ wallet_address: string }`
- **Aturan Bisnis:**
  - Jika `delta < 24 jam`: Tolak dengan status 400 dan pesan cooldown.
  - Jika `24 <= delta <= 48 jam`: Streak bertambah 1.
  - Jika `delta > 48 jam`: Streak direset ke 1.
  - Poin dihitung dengan multiplier: `100 * (1 + (streak - 1) * 0.25)`.
- **Atomic Transaction:** Update `users` dan insert record ke `points_events`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menolak klaim ganda dalam durasi kurang dari 24 jam.
- [x] Menghitung streak dan bonus multiplier secara presisi.
- [x] Mencatat log audit transaksi poin ke points_events.
- [x] Unit test API route checkin lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/checkin/route.ts`
- `omen/web/tests/api-checkin.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan serverless Next.js API route handler `POST /api/checkin` di `omen/web/app/api/checkin/route.ts`.
  2. Mengimplementasikan evaluasi delta waktu dari `last_checkin_at`: penolakan klaim ganda < 24 jam (status 400), penambahan streak jika 24 <= delta <= 48 jam, dan reset streak ke 1 jika delta > 48 jam atau check-in perdana.
  3. Mengimplementasikan formula bonus multiplier poin: `100 * (1 + (streak - 1) * 0.25)`.
  4. Melakukan pembaruan profil akumulasi poin dan timestamp `last_checkin_at` pada tabel `users`, serta pencatatan audit log transaksi poin ke tabel `points_events` dengan `source: 'daily_checkin'`.
  5. Menulis unit test komprehensif di `omen/web/tests/api-checkin.test.ts` (8 skenario uji: validasi input, 404 user, check-in perdana, cooldown < 24 jam, bonus multiplier streak, reset streak > 48 jam, error handling, dan Zero-Comment Policy).
  6. Memvalidasi seluruh test suite Vitest `npm run test` (26 file, 156 test lolos 100%) dan type check `npx tsc --noEmit` lolos tanpa error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/checkin/route.ts` (Created)
  - `omen/web/tests/api-checkin.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-26-api-daily-checkin-streak.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Tanggal dan waktu check-in dinormalisasi ke format ISO-8601 UTC string (`TIMESTAMPTZ`) untuk konsistensi penyimpanan database global sesuai `global-guidelines/database.md`.
