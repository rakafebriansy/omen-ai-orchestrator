---
id: TICKET-26
title: Pembuatan API Route Daily Check-in Streak
status: Todo
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
- [ ] Menolak klaim ganda dalam durasi kurang dari 24 jam.
- [ ] Menghitung streak dan bonus multiplier secara presisi.
- [ ] Mencatat log audit transaksi poin ke points_events.
- [ ] Unit test API route checkin lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/checkin/route.ts`
- `omen/web/tests/api-checkin.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
