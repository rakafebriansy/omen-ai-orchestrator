---
id: TICKET-16
title: Pembuatan Tabel Riwayat Taruhan Pengguna
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen tabel riwayat taruhan `UserBetsTable` di `omen/web/components/UserBetsTable.tsx` yang merinci seluruh posisi taruhan aktif maupun riwayat masa lalu milik pengguna.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`UserBetsTable.tsx`)
1. **Kontainer Tabel:**
   - `bg-white border border-border-subtle rounded-2xl overflow-hidden shadow-sm`.
2. **Header Kolom:**
   - `bg-bg-subtle text-text-muted text-xs font-mono font-semibold uppercase py-3.5 px-6 border-b border-border-subtle`.
   - Kolom: "Market Title", "Side Selected", "Amount Staked", "Status / Outcome", "Action".
3. **Baris Data:**
   - Side Badge: Badge Yes (Hijau) atau No (Merah).
   - Amount: Format nominal ETH font mono (contoh: "0.25 ETH").
   - Status Badge: "Active" (Biru), "Won" (Hijau), "Lost" (Merah), atau "Cancelled" (Abu-abu).
   - Action Slot: Memuat tombol klaim payout jika status taruhan menang.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Tabel menampilkan daftar taruhan pengguna secara terstruktur.
- [ ] Badge status kubu dan hasil taruhan memiliki warna yang kontras.
- [ ] Unit test komponen UserBetsTable lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/UserBetsTable.tsx`
- `omen/web/tests/user-bets-table.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
