---
id: TICKET-18
title: Pembuatan Halaman My Bets
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun halaman penuh My Bets di `omen/web/app/my-bets/page.tsx` yang memadukan ringkasan portofolio taruhan pribadi pengguna dan daftar tabel riwayat taruhan `UserBetsTable`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Halaman (`app/my-bets/page.tsx`)
1. **Header Halaman:**
   - Judul H1: "My Predictions dan Bets" (`text-3xl sm:text-4xl font-extrabold text-accent-navy tracking-tight`).
   - Subjudul ringkasan performa taruhan.
2. **Portofolio Summary Cards (3 Kartu):**
   - `grid grid-cols-1 sm:grid-cols-3 gap-4 mb-8`.
   - Kartu 1: "Total ETH Staked" (contoh: "1.20 ETH").
   - Kartu 2: "Total Payouts Won" (contoh: "2.45 ETH").
   - Kartu 3: "Win Rate" (contoh: "75.0%").
3. **Tabel Riwayat Taruhan:**
   - Integrasi komponen `UserBetsTable` dan tombol `ClaimPayoutButton`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Halaman merender 3 kartu statistik portofolio dan tabel riwayat taruhan.
- [ ] Menampilkan empty state ramah jika pengguna belum pernah bertaruh.
- [ ] Unit test halaman my-bets berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/my-bets/page.tsx`
- `omen/web/tests/my-bets-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
