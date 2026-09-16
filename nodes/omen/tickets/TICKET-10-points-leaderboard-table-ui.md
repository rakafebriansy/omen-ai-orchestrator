---
id: TICKET-10
title: Pembuatan Tabel Ranking Leaderboard Poin
status: Done
priority: Medium
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen tabel peringkat `LeaderboardTable` di `omen/web/components/LeaderboardTable.tsx` yang menampilkan urutan ranking global dompet berdasarkan akumulasi total poin, jumlah streak, dan status podium.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`LeaderboardTable.tsx`)
1. **Kontainer Tabel:**
   - `bg-white border border-border-subtle rounded-2xl overflow-hidden shadow-sm`.
2. **Header Kolom:**
   - `bg-bg-subtle text-text-muted text-xs font-mono font-semibold uppercase tracking-wider py-3.5 px-6 border-b border-border-subtle`.
   - Kolom: "Rank", "Wallet Address", "Streak Days", "Total Points".
3. **Baris Data (Row Item):**
   - Baris umum: `py-4 px-6 border-b border-slate-100 hover:bg-bg-subtle/80 transition-colors flex items-center justify-between sm:table-row`.
   - **Podium Rank Icons (Rank 1, 2, 3):**
     - Rank 1: Badge emas `bg-amber-100 text-amber-800 font-bold px-2.5 py-0.5 rounded-full font-mono`.
     - Rank 2: Badge perak `bg-slate-200 text-slate-700 font-bold px-2.5 py-0.5 rounded-full font-mono`.
     - Rank 3: Badge perunggu `bg-amber-50 text-amber-900 border border-amber-200 font-bold px-2.5 py-0.5 rounded-full font-mono`.
   - **Baris Milik Pengguna (Current User Row):**
     - Diberi highlight `bg-primary-blue-soft/50 border-l-4 border-l-primary-blue`.
4. **Paginasi Baris Bawah:**
   - Tombol navigasi Previous dan Next dengan indikator halaman aktif.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Tabel merender header kolom dan baris data dengan penataan rapi.
- [x] Visual podium 1-3 tampil dengan badge warna khusus.
- [x] Baris pengguna yang sedang terhubung mendapat highlight visual yang jelas.
- [x] Unit test komponen LeaderboardTable lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/LeaderboardTable.tsx`
- `omen/web/tests/leaderboard-table.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat komponen tabel peringkat `LeaderboardTable.tsx` dengan dukungan podium 1-3 (*Gold, Silver, Bronze badges*), avatar inisial/ENS name, badge streak harian, multiplier, dan total poin terakumulasi.
  2. Mengimplementasikan penandaan kontras pada baris akun pengguna aktif (`isCurrentUser`) dengan highlight `bg-primary-blue/15 border-l-4 border-l-primary-blue` dan badge "YOU".
  3. Membangun kontrol baris paginasi bawah (*Previous/Next*) dengan indikator hitungan halaman dan batas slicing data.
  4. Menyusun test suite `tests/leaderboard-table.test.tsx` dengan 4 unit tests Vitest mencakup verifikasi render tabel, styling podium, highlight current user, dan navigasi paginasi (total 52/52 tests pass 100%).
  5. Menjalankan type checking `npx tsc --noEmit` (0 error) dan verifikasi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/LeaderboardTable.tsx` [Created]
  - `omen/web/tests/leaderboard-table.test.tsx` [Created]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Tabel dirancang menerima data array `LeaderboardEntry[]` via props sehingga langsung kompatibel dengan endpoint leaderboard API `/api/leaderboard` pada tiket backend Fase 2.
