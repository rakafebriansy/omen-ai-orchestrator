---
id: TICKET-07
title: Pembuatan Widget Daily Check-in Streak
status: Done
priority: Medium
labels: [Frontend, UI, Gamification]
---

# Deskripsi
Membangun komponen widget interaktif `DailyCheckinWidget` di `omen/web/components/DailyCheckinWidget.tsx` yang menampilkan kalender visual streak 7 hari, akumulasi bonus multiplier, tombol klaim harian dengan status cooldown countdown, serta animasi reward poin.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`DailyCheckinWidget.tsx`)
1. **Wadah Utama:**
   - `bg-white border border-border-subtle rounded-2xl p-6 sm:p-8 shadow-sm`.
2. **Header Widget:**
   - Judul: "Daily Check-in Streak" (`text-xl font-bold text-accent-navy flex items-center gap-2`).
   - Ikon Api / Flame: Ikon api oranye berlatar `bg-warning-soft text-warning-amber p-1.5 rounded-lg`.
   - Multiplier Badge: `bg-primary-blue-soft text-primary-blue font-mono font-bold text-xs px-2.5 py-1 rounded-full border border-primary-blue/20` (contoh: "1.5x Multiplier Active").
3. **Pelacak Streak 7 Hari (7-Day Grid Tracker):**
   - Grid 7 kolom: `grid grid-cols-7 gap-2 sm:gap-3 my-6`.
   - Item Hari (`Day 1` s/d `Day 7`):
     - *State Sudah Klaim (Checked):* `bg-yes-green-soft border border-yes-green/30 text-yes-green rounded-xl p-3 text-center font-mono font-bold`.
     - *State Hari Ini (Current Active):* `bg-primary-blue-soft border-2 border-primary-blue text-primary-blue rounded-xl p-3 text-center font-mono font-bold shadow-xs`.
     - *State Terkunci (Upcoming):* `bg-bg-subtle border border-border-subtle text-text-muted rounded-xl p-3 text-center font-mono`.
4. **Tombol Aksi Klaim:**
   - *State Siap Klaim:* Tombol CTA lebar `w-full bg-primary-blue text-white hover:bg-primary-blue-hover py-3.5 rounded-xl font-bold text-base shadow-sm transition-all`.
   - *State Cooldown:* Tombol disabled `w-full bg-bg-subtle text-text-muted border border-border-subtle py-3.5 rounded-xl font-mono text-sm cursor-not-allowed` menampilkan waktu hitung mundur (contoh: "Next Check-in in 14h 22m 10s").

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Merender tracker 7 hari dengan indikator visual hari checked, aktif, dan terkunci.
- [x] Menampilkan countdown cooldown timer jika check-in hari ini sudah selesai.
- [x] Tombol klaim memicu callback interaktif dengan feedback visual yang responsif.
- [x] Aksesibilitas ARIA label pada indikator streak count dan waktu cooldown.
- [x] Unit test komponen DailyCheckinWidget lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/DailyCheckinWidget.tsx`
- `omen/web/tests/checkin-widget.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat komponen gamifikasi `DailyCheckinWidget.tsx` dengan visualisasi 7-day streak matrix (checked, current active, locked), badge streak multiplier, live timer cooldown countdown, dan notifikasi perolehan reward poin.
  2. Memasang aksesibilitas WAI-ARIA (`role="region"`, `aria-label="Daily Check-in Streak"`, `aria-live="polite"` pada counter timer).
  3. Menyusun test suite `tests/checkin-widget.test.tsx` dengan unit test Vitest mencakup verifikasi render 7-day grid, interaksi claim tombol, status perolehan poin, countdown interval timer, dan initial cooldown state (total 40/40 tests pass 100%).
  4. Menjalankan type check `npx tsc --noEmit` (0 error) dan verifikasi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/DailyCheckinWidget.tsx` [Created]
  - `omen/web/tests/checkin-widget.test.tsx` [Created]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Komponen menerima props dinamis `pointsSchedule`, `currentStreak`, dan callback `onCheckIn` yang siap disambungkan ke endpoint API `/api/checkin` dan Supabase streak tracking pada tiket backend Fase 2.
