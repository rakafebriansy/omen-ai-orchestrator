---
id: TICKET-09
title: Pembuatan Halaman Quests dan Farming
status: Done
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
- [x] Halaman memadukan ringkasan saldo poin, DailyCheckinWidget, dan daftar QuestCard secara terstruktur.
- [x] Tab kategori filter menyaring daftar misi secara interaktif.
- [x] Tampilan sepenuhnya responsif dan bersih di seluruh resolusi layar.
- [x] Unit test halaman quests berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/quests/page.tsx`
- `omen/web/tests/quests-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun halaman `app/quests/page.tsx` dengan integrasi kartu saldo akumulasi poin (`2,450 PTS`), tier ranking badge (*Tier II • Silver Hunter*), stat boxes (Quests Done, Active Streak, Airdrop Rank), `<DailyCheckinWidget />`, serta direktori katalog misi.
  2. Mengembangkan filter kategori tab interaktif (*All Quests, Onboarding, Social, On-Chain, Daily*) dengan badge counter jumlah misi dinamis dan empty state handling.
  3. Mengintegrasikan update saldo poin dinamis ketika pengguna menyelesaikan misi pada `QuestCard` atau melakukan daily check-in.
  4. Menyusun test suite `tests/quests-page.test.tsx` mencakup 4 unit test Vitest untuk render halaman, navigasi filter kategori, dan akumulasi penambahan poin saat aksi quest dieksekusi (total 48/48 tests pass 100%).
  5. Menjalankan type checking `npx tsc --noEmit` (0 error) dan verifikasi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/quests/page.tsx` [Created]
  - `omen/web/tests/quests-page.test.tsx` [Created]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Struktur data quest dirancang modular sehingga saat API `/api/quests` terhubung pada Fase 2, komponen tinggal menerima data via SWR/TanStack Query tanpa merombak UI.
