---
id: TICKET-13
title: Pembuatan Komponen Kartu Pasar Prediksi
status: Done
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen kartu pasar prediksi `MarketCard` di `omen/web/components/MarketCard.tsx` dengan progress bar persentase odds Yes/No, penghitung mundur batas waktu, serta tombol aksi taruhan dua arah.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`MarketCard.tsx`)
1. **Wadah Kartu:**
   - `bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 rounded-2xl p-6 shadow-sm hover:border-emerald-500/50 dark:hover:border-emerald-500/50 hover:shadow-md transition-all flex flex-col justify-between`.
2. **Header Kartu:**
   - Badge Kategori (contoh: "CRYPTO") dan Badge Status ("Active" hijau dengan pulse, "Closing Soon" oranye, atau "Resolved").
   - Label Waktu: Countdown timer format `Ends in 1d 14h` berfont mono.
3. **Pertanyaan Prediksi:**
   - `text-lg font-bold text-zinc-900 dark:text-zinc-100 leading-snug my-2 line-clamp-2`.
4. **Implied Odds dan Pool Progress Bar:**
   - Bilah ganda: Bagian kiri `bg-emerald-500` (Yes), bagian kanan `bg-rose-500` (No).
   - Label persentase di atas bar: "Yes X%" vs "No Y%".
   - Total Pool dan Volume: "Total Pool: X ETH" dan "Vol: Y ETH".
5. **Tombol Aksi Cepat (Quick Bet Buttons):**
   - Tombol YES: `flex-1 bg-emerald-50 dark:bg-emerald-950/40 text-emerald-600 dark:text-emerald-400 hover:bg-emerald-100 dark:hover:bg-emerald-900/50 border border-emerald-500/20 py-2.5 rounded-xl font-bold text-sm transition-all`.
   - Tombol NO: `flex-1 bg-rose-50 dark:bg-rose-950/40 text-rose-600 dark:text-rose-400 hover:bg-rose-100 dark:hover:bg-rose-900/50 border border-rose-500/20 py-2.5 rounded-xl font-bold text-sm transition-all`.
   - Resolusi: Banner status pemenang pasar jika pasar telah `resolved`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Kartu menampilkan judul prediksi, batas waktu, dan total pool secara presisi.
- [x] Progress bar rasio odds merender persentase Yes dan No dengan warna kontras.
- [x] Tombol Yes dan No memicu callback pemilihan sisi pasar.
- [x] Unit test komponen MarketCard lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/MarketCard.tsx`
- `omen/web/tests/market-card.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan komponen `MarketCard.tsx` dengan badge kategori semantik, live status pulse (Active / Closing Soon / Resolved), countdown timer waktu, dual odds progress bar Yes/No, metrik total pool likuiditas & volume, serta tombol interaktif Bet YES dan Bet NO.
  2. Menyusun unit test suite `market-card.test.tsx` dengan 5 skenario pengujian lengkap menguji rendering detail kartu, eksekusi tombol Bet YES, eksekusi tombol Bet NO dengan passing parameter `outcome` dan `market`, badge closing-soon, dan state resolved.
  3. Memverifikasi seluruh pengujian Vitest (total 65/65 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/MarketCard.tsx` [Created]
  - `omen/web/tests/market-card.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-13-prediction-market-card-ui.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan CSS transition halus pada bilah progress bar dual-color (`transition-all duration-500`) dan penanganan status pasar selesai (`resolved`) yang otomatis menonaktifkan aksi taruhan dengan menampilkan ringkasan pemenang.
