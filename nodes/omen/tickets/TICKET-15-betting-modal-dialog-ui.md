---
id: TICKET-15
title: Pembuatan Modal Dialog Pasang Taruhan
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun modal dialog interaktif `BettingModal` di `omen/web/components/BettingModal.tsx` yang memfasilitasi pengguna memilih sisi taruhan (Yes/No), memasukkan nominal Native ETH, menghitung estimasi return secara instan, dan mengonfirmasi transaksi.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`BettingModal.tsx`)
1. **Backdrop dan Kontainer Modal:**
   - Backdrop: `fixed inset-0 bg-accent-navy/40 backdrop-blur-sm z-50 flex items-center justify-center p-4`.
   - Wadah: `bg-white border border-border-subtle rounded-2xl max-w-lg w-full p-6 sm:p-8 shadow-2xl relative`.
2. **Header Modal:**
   - Judul pasar prediksi yang dipilih.
   - Tombol tutup silang (X) di sudut kanan atas dengan `aria-label="Close betting modal"`.
3. **Toggle Sisi Pilihan (Yes / No):**
   - Segmented control 2 tombol:
     - Sisi Yes: `bg-yes-green text-white` saat aktif.
     - Sisi No: `bg-no-red text-white` saat aktif.
4. **Input Nominal Taruhan:**
   - Input field numerik Native ETH berfont mono besar `text-2xl font-extrabold text-accent-navy`.
   - Tombol preset cepat: "+0.01 ETH", "+0.05 ETH", "+0.1 ETH", "MAX".
5. **Kalkulator Estimasi Payout (Live Return Calculator):**
   - Kotak rincian: `bg-bg-subtle border border-border-subtle rounded-xl p-4 my-4 space-y-2 text-sm`.
   - Baris 1: "Current Implied Odds" (contoh: "65.0%").
   - Baris 2: "Potential Return" (`text-base font-bold font-mono text-yes-green` contoh: "0.154 ETH (+54%)").
6. **Tombol Submit:**
   - "Confirm Bet (0.1 ETH)" (`w-full bg-primary-blue text-white hover:bg-primary-blue-hover py-3.5 rounded-xl font-bold text-base shadow-sm transition-all`).

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Modal dapat dibuka dan ditutup dengan tombol close atau klik backdrop.
- [ ] Kalkulator instan memperbarui potensi return saat nominal ETH diubah.
- [ ] Validasi form mencegah input kosong atau bernilai negatif.
- [ ] Unit test komponen BettingModal lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/BettingModal.tsx`
- `omen/web/tests/betting-modal.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
