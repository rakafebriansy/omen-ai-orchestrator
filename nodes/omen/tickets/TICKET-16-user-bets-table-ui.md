---
id: TICKET-16
title: Pembuatan Tabel Riwayat Taruhan Pengguna
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen tabel riwayat taruhan `UserBetsTable` di `omen/web/components/UserBetsTable.tsx` yang merinci seluruh posisi taruhan aktif maupun riwayat masa lalu milik pengguna.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`UserBetsTable.tsx`)
1. **Kontainer Tabel:**
   - `bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 rounded-2xl overflow-hidden shadow-sm w-full`.
2. **Header Kolom:**
   - `bg-zinc-50/80 dark:bg-zinc-800/50 text-zinc-500 dark:text-zinc-400 text-[11px] font-mono font-semibold uppercase py-3.5 px-6 border-b border-zinc-200 dark:border-zinc-800`.
   - Kolom: "Market Question", "Side", "Staked", "Potential Return", "Status", "Action".
3. **Baris Data:**
   - Side Badge: Badge Yes (Emerald) atau No (Rose).
   - Amount & Return: Format nominal ETH font mono (contoh: "0.25 ETH" dan "0.48 ETH (+92% ROI)").
   - Status Badge: "Active" (Sky), "Won 🏆" (Emerald), "Lost" (Rose), atau "Cancelled" (Zinc).
   - Action Slot: Tombol "Claim Payout" jika menang dan belum diklaim, atau badge "Claimed ✓".

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Tabel menampilkan daftar taruhan pengguna secara terstruktur.
- [x] Badge status kubu dan hasil taruhan memiliki warna yang kontras.
- [x] Unit test komponen UserBetsTable lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/UserBetsTable.tsx`
- `omen/web/tests/user-bets-table.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun komponen tabel `UserBetsTable.tsx` dengan header kolom informatif, baris data posisi taruhan dengan badge kontras (YES/NO), perhitungan return/ROI, status label (Active, Won, Lost, Cancelled), action slot tombol Claim Payout / Claimed badge, dan tampilan empty state terintegrasi link `/predictions`.
  2. Menyusun test suite unit testing Vitest `user-bets-table.test.tsx` dengan 5 skenario pengujian komprehensif menguji rendering struktur tabel & baris, rendering badge kubu & status, eksekusi tombol Claim Payout memicu callback `onClaimPayout`, verifikasi status Claimed, dan rendering empty state.
  3. Memverifikasi seluruh test suite Vitest (total 83/83 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/UserBetsTable.tsx` [Created]
  - `omen/web/tests/user-bets-table.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-16-user-bets-table-ui.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan layout table HTML semantik dengan pembagian cell responsif (`overflow-x-auto`) dan skeleton loading pulse ketika `isLoading=true` untuk pengalaman interaktif yang mulus.
