---
id: TICKET-09
title: Pembuatan Halaman Quests dan Farming
status: Todo
priority: Medium
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman penuh Quests dan Points Farming di `omen/web/app/quests/page.tsx` yang menyatukan widget Daily Check-in Streak, kartu rangkuman total saldo poin pengguna, filter tab kategori misi, serta daftar komponen QuestCard.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Halaman (`app/quests/page.tsx`)
1. **Header Halaman:**
   - Judul H1: "Quests dan Points Farming" (`text-3xl sm:text-4xl font-extrabold text-accent-navy tracking-tight`).
   - Deskripsi: "Complete daily activities and on-chain predictions to accumulate ecosystem reward points."
2. **Ringkasan Saldo Poin:**
   - Kartu highlight atas: `bg-gradient-to-r from-primary-blue-soft to-bg-subtle border border-primary-blue/20 rounded-2xl p-6 flex flex-wrap items-center justify-between gap-4`.
   - Menampilkan total poin terkini dengan tipografi besar `text-4xl font-extrabold font-mono text-primary-blue`.
3. **Seksi Daily Check-in:**
   - Merender komponen `DailyCheckinWidget`.
4. **Seksi Direktori Quests:**
   - Tab Filter: "All Quests", "Onboarding", "Social Tasks", "Prediction Tasks".
   - Daftar Kartu: Render vertikal komponen `QuestCard` dengan jarak `space-y-4`.
   - Empty State: Ilustrasi dan teks ramah jika tidak ada misi pada kategori yang dipilih.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Halaman memadukan ringkasan saldo poin, DailyCheckinWidget, dan daftar QuestCard secara terstruktur.
- [ ] Tab kategori filter menyaring daftar misi secara interaktif.
- [ ] Tampilan sepenuhnya responsif dan bersih di seluruh resolusi layar.
- [ ] Unit test halaman quests berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/quests/page.tsx`
- `omen/web/tests/quests-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
