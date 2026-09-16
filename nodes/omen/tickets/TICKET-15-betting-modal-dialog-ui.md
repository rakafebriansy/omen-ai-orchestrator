---
id: TICKET-15
title: Pembuatan Modal Dialog Pasang Taruhan
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun modal dialog interaktif `BettingModal` di `omen/web/components/BettingModal.tsx` yang memfasilitasi pengguna memilih sisi taruhan (Yes/No), memasukkan nominal Native ETH, menghitung estimasi return secara instan, dan mengonfirmasi transaksi.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`BettingModal.tsx`)
1. **Backdrop dan Kontainer Modal:**
   - Backdrop: `fixed inset-0 bg-black/75 backdrop-blur-sm z-50 flex items-center justify-center p-4 overflow-y-auto`.
   - Wadah: `bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 rounded-2xl max-w-lg w-full p-6 sm:p-8 shadow-2xl relative text-zinc-900 dark:text-zinc-100`.
2. **Header Modal:**
   - Judul pasar prediksi yang dipilih, kategori, batas waktu, dan tombol tutup silang (X) dengan `aria-label="Close betting modal"`.
3. **Toggle Sisi Pilihan (Yes / No):**
   - Segmented control 2 tombol dengan highlight aktif Emerald untuk YES dan Rose untuk NO beserta persentase odds.
4. **Input Nominal Taruhan:**
   - Input field numerik Native ETH berfont mono besar dengan tombol preset cepat: `+0.01`, `+0.05`, `+0.10`, dan `MAX`.
5. **Kalkulator Estimasi Payout (Live Return Calculator):**
   - Rincian kalkulasi: Current Implied Odds, Protocol Fee (1%), Potential Payout (ETH), dan Estimated ROI percentage (+% ROI).
6. **Tombol Submit:**
   - "Confirm Bet (X ETH)" dengan state loading transaksi dan penanganan disabled validation saat amount <= 0 atau melebihi saldo.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Modal dapat dibuka dan ditutup dengan tombol close atau klik backdrop.
- [x] Kalkulator instan memperbarui potensi return saat nominal ETH diubah.
- [x] Validasi form mencegah input kosong atau bernilai negatif.
- [x] Unit test komponen BettingModal lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/BettingModal.tsx`
- `omen/web/tests/betting-modal.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun komponen modal dialog `BettingModal.tsx` yang mendukung toggle outcome dua arah (YES/NO), input amount numerik responsif, tombol preset nominal cepat (+0.01, +0.05, +0.10, MAX), kalkulator estimasi return real-time, validasi saldo & batas minimum, dan callback submit async `onConfirmBet`.
  2. Menyusun test suite unit testing Vitest `betting-modal.test.tsx` dengan 8 skenario pengujian komprehensif (render saat open/close, render rincian pasar & saldo, toggle outcome, preset amount & MAX, kalkulasi payout dinamis, penanganan error validasi saldo, eksekusi submit valid, dan trigger close via tombol/backdrop).
  3. Memverifikasi seluruh test suite Vitest (total 78/78 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/BettingModal.tsx` [Created]
  - `omen/web/tests/betting-modal.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-15-betting-modal-dialog-ui.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Komponen menyertakan listener tombol Escape keyboard (`keydown`) dan backdrop click handler untuk pengalaman pengguna modal yang aksesibel dan ergonomis di seluruh perangkat.
