---
id: TICKET-08
title: Pembuatan Komponen Kartu Quest
status: Todo
priority: Medium
labels: [Frontend, UI, Gamification]
---

# Deskripsi
Membangun komponen baris/kartu misi `QuestCard` di `omen/web/components/QuestCard.tsx` yang menyajikan detail instruksi tugas, perolehan poin reward, kategori misi, serta tombol interaksi verifikasi.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`QuestCard.tsx`)
1. **Wadah Kartu:**
   - `bg-white border border-border-subtle rounded-xl p-5 sm:p-6 shadow-sm hover:border-slate-300 hover:shadow-md transition-all flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4`.
2. **Informasi Tugas (Sisi Kiri):**
   - Kategori Tag: `text-xs font-mono font-semibold uppercase text-text-muted tracking-wider` (contoh: "SOCIAL", "ON-CHAIN", "ONBOARDING").
   - Judul Misi: `text-base sm:text-lg font-bold text-accent-navy mt-1`.
   - Deskripsi: `text-sm text-text-muted mt-1 leading-normal max-w-xl`.
3. **Reward dan Tombol Aksi (Sisi Kanan):**
   - Badge Poin: `flex items-center gap-1.5 bg-primary-blue-soft text-primary-blue font-mono font-bold text-sm px-3 py-1.5 rounded-lg border border-primary-blue/20` (contoh: "+100 PTS").
   - Tombol Aksi:
     - *State Tersedia (Available):* `bg-primary-blue text-white hover:bg-primary-blue-hover px-5 py-2 rounded-lg font-semibold text-sm transition-all`.
     - *State Memproses (Verifying):* `bg-bg-subtle text-text-muted border border-border-subtle px-5 py-2 rounded-lg font-medium text-sm flex items-center gap-2`.
     - *State Selesai (Completed / Claimed):* `bg-yes-green-soft text-yes-green border border-yes-green/20 px-4 py-2 rounded-lg font-semibold text-sm flex items-center gap-1.5` bertuliskan "Completed".

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Merender badge reward poin dengan nilai yang jelas.
- [ ] Menampilkan status misi secara akurat (Tersedia, Verifikasi, atau Selesai).
- [ ] Tombol memicu event callback aksi verifikasi saat diklik.
- [ ] Unit test komponen QuestCard lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/QuestCard.tsx`
- `omen/web/tests/quest-card.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
