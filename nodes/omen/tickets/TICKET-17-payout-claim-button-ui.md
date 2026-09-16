---
id: TICKET-17
title: Pembuatan Komponen Tombol Klaim Payout
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen tombol penarikan hadiah kemenangan `ClaimPayoutButton` di `omen/web/components/ClaimPayoutButton.tsx` dengan indikator saldo reward yang siap dicairkan.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`ClaimPayoutButton.tsx`)
1. **State Siap Klaim (Claimable):**
   - Tombol aktif `bg-emerald-600 hover:bg-emerald-700 dark:bg-emerald-500 text-white dark:text-zinc-950 px-4 py-2 rounded-lg font-bold text-xs font-mono shadow-xs transition-all flex items-center justify-center gap-1.5 active:scale-98`.
   - Teks: "Claim {amount} ETH".
2. **State Memproses (Claiming):**
   - Tombol disabled dengan spinner loading berputar dan teks "Claiming...".
3. **State Sudah Diklaim (Claimed):**
   - Badge pasif `bg-zinc-100 dark:bg-zinc-800 text-zinc-500 dark:text-zinc-400 border border-zinc-200 dark:border-zinc-700/60 px-3 py-1.5 rounded-lg text-xs font-mono font-medium` berlabel "Claimed ✓".

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Tombol aktif khusus untuk posisi taruhan menang yang belum ditarik.
- [x] Menampilkan estimasi jumlah dana ETH yang akan diklaim.
- [x] Unit test komponen ClaimPayoutButton lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/ClaimPayoutButton.tsx`
- `omen/web/tests/claim-button.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun komponen tombol aksi `ClaimPayoutButton.tsx` dengan 3 state visual utama: Siap Klaim (Claimable) dengan nominal reward ETH, Memproses Transaksi (Claiming) dengan visual spinner dan disabled state, serta Sudah Diklaim (Claimed) dengan badge pasif checkmark.
  2. Menyusun test suite unit testing Vitest `claim-button.test.tsx` dengan 4 skenario pengujian komprehensif menguji rendering tombol dengan nominal ETH, eksekusi klik async memicu callback `onClaim` dan transisi state claiming, rendering badge state Claimed, dan perilaku tombol ketika disabled.
  3. Memverifikasi seluruh test suite Vitest (total 87/87 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/ClaimPayoutButton.tsx` [Created]
  - `omen/web/tests/claim-button.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-17-payout-claim-button-ui.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Komponen mendukung pengelolaan internal loading state ketika callback `onClaim` mengembalikan Promise async, sehingga siap diintegrasikan langsung dengan Web3 Wagmi contract claim hook di fase berikutnya.
