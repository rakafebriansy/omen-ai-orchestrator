---
id: TICKET-13
title: Pembuatan Komponen Kartu Pasar Prediksi
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen kartu pasar prediksi `MarketCard` di `omen/web/components/MarketCard.tsx` dengan progress bar persentase odds Yes/No, penghitung mundur batas waktu, serta tombol aksi taruhan dua arah.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`MarketCard.tsx`)
1. **Wadah Kartu:**
   - `bg-white border border-border-subtle rounded-2xl p-6 shadow-sm hover:border-slate-300 hover:shadow-md transition-all flex flex-col justify-between`.
2. **Header Kartu:**
   - Badge Kategori (contoh: "CRYPTO") dan Badge Status ("Active" hijau atau "Closing Soon" oranye).
   - Label Waktu: Countdown timer format `Ends in 1d 14h` berfont mono.
3. **Pertanyaan Prediksi:**
   - `text-lg font-bold text-accent-navy leading-snug my-3 line-clamp-2`.
4. **Implied Odds dan Pool Progress Bar:**
   - Bilah ganda: Bagian kiri `bg-yes-green` (Yes), bagian kanan `bg-no-red` (No).
   - Label persentase di atas bar: "Yes 65%" vs "No 35%".
   - Total Pool: "Total Pool: 8.45 ETH" (`text-xs font-mono text-text-muted mt-2`).
5. **Tombol Aksi Cepat (Quick Bet Buttons):**
   - Tombol YES: `flex-1 bg-yes-green-soft text-yes-green hover:bg-emerald-100 border border-yes-green/20 py-2.5 rounded-xl font-bold text-sm transition-all`.
   - Tombol NO: `flex-1 bg-no-red-soft text-no-red hover:bg-rose-100 border border-no-red/20 py-2.5 rounded-xl font-bold text-sm transition-all`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Kartu menampilkan judul prediksi, batas waktu, dan total pool secara presisi.
- [ ] Progress bar rasio odds merender persentase Yes dan No dengan warna kontras.
- [ ] Tombol Yes dan No memicu callback pemilihan sisi pasar.
- [ ] Unit test komponen MarketCard lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/MarketCard.tsx`
- `omen/web/tests/market-card.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
