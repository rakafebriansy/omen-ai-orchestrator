---
id: TICKET-07
title: Pembuatan Widget Daily Check-in Streak
status: Todo
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
- [ ] Merender tracker 7 hari dengan indikator visual hari checked, aktif, dan terkunci.
- [ ] Menampilkan countdown cooldown timer jika check-in hari ini sudah selesai.
- [ ] Tombol klaim memicu callback interaktif dengan feedback visual yang responsif.
- [ ] Aksesibilitas ARIA label pada indikator streak count dan waktu cooldown.
- [ ] Unit test komponen DailyCheckinWidget lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/DailyCheckinWidget.tsx`
- `omen/web/tests/checkin-widget.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
