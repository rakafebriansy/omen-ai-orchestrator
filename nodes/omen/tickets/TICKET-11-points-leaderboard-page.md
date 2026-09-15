---
id: TICKET-11
title: Pembuatan Halaman Leaderboard
status: Todo
priority: Medium
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman penuh Leaderboard di `omen/web/app/leaderboard/page.tsx` yang memuat kartu personal ranking summary di bagian atas dan tabel peringkat global di bawahnya.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Halaman (`app/leaderboard/page.tsx`)
1. **Header Halaman:**
   - Judul H1: "Points Leaderboard" (`text-3xl sm:text-4xl font-extrabold text-accent-navy tracking-tight`).
   - Deskripsi: "Global rankings of all active participants based on points earned from check-ins and prediction markets."
2. **Kartu Rangkuman Personal (Top Summary Card):**
   - `grid grid-cols-1 sm:grid-cols-3 gap-4 bg-white border border-border-subtle rounded-2xl p-6 shadow-sm mb-8`.
   - Metrik 1: "Your Current Rank" (contoh: "#14").
   - Metrik 2: "Your Total Points" (contoh: "3,450 PTS").
   - Metrik 3: "Gap to Next Tier" (contoh: "120 PTS needed").
3. **Pencarian dan Tabel Peringkat:**
   - Input search wallet address di atas tabel.
   - Integrasi komponen `LeaderboardTable`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Halaman merender kartu metrik personal dan tabel leaderboard global secara terstruktur.
- [ ] Tersedia input pencarian untuk menyaring alamat dompet tertentu.
- [ ] Unit test halaman leaderboard berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/leaderboard/page.tsx`
- `omen/web/tests/leaderboard-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
