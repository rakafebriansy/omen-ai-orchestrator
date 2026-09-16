---
id: TICKET-19
title: Pembuatan Form Admin Pembuatan Pasar Prediksi
status: Done
priority: Medium
labels: [Frontend, Admin, UI]
---

# Deskripsi
Membangun formulir antarmuka admin `AdminMarketCreateForm` di `omen/web/components/AdminMarketCreateForm.tsx` untuk mendaftarkan pasar prediksi baru beserta live preview kartu pasar.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`AdminMarketCreateForm.tsx`)
1. **Tata Letak Formulir (Form Grid):**
   - Grid dwi-kolom responsif: Formulir isian di panel kiri dan sticky live preview di panel kanan berbalut `bg-white dark:bg-zinc-900 border border-zinc-200 dark:border-zinc-800 rounded-2xl p-6 sm:p-8 shadow-sm`.
2. **Field Masukan (Input Fields):**
   - Field Judul Prediksi: Input teks wajib validasi minimal 5 karakter.
   - Field Kategori: Dropdown select (CRYPTO, MEME, TRENDING, L2, MACRO).
   - Field Deadline: Date & Time picker dengan validasi waktu di masa depan.
   - Field Seed Liquidity: Input numerik ETH pool awal.
   - Field Sumber Resolusi: Input URL referensi oracle / berita.
3. **Live Card Preview:**
   - Panel samping interaktif yang merender komponen `MarketCard` secara instan dan reaktif sesuai perubahan isian formulir.
4. **Tombol Submit:**
   - "Publish Market to Blockchain" dengan status loading spinner saat transaksi diproses.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Formulir memvalidasi seluruh input wajib dan batas waktu minimal 1 jam di masa depan.
- [x] Live preview merender kartu pasar secara interaktif.
- [x] Unit test komponen AdminMarketCreateForm lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketCreateForm.tsx`
- `omen/web/tests/admin-create-form.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membangun komponen formulir admin `AdminMarketCreateForm.tsx` yang dilengkapi field input lengkap (judul pasar, kategori select, date/time deadline, seed liquidity, resolution URL), validasi kelayakan batas waktu masa depan & nominal likuiditas, panel sticky *Live Card Preview* berbasis `<MarketCard />`, serta penanganan submit async.
  2. Menyusun test suite unit testing Vitest `admin-create-form.test.tsx` dengan 4 skenario pengujian komprehensif menguji render form & preview card, interaktivitas live typing update pada preview, validasi deadline lampau, serta eksekusi submit valid memicu callback `onSubmitMarket`.
  3. Memverifikasi seluruh test suite Vitest (total 94/94 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/AdminMarketCreateForm.tsx` [Created]
  - `omen/web/tests/admin-create-form.test.tsx` [Created]
  - `nodes/omen/tickets/TICKET-19-admin-market-create-form-ui.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan `useMemo` untuk membangun state `previewMarketData` secara instan tanpa re-render berlebih, serta struktur form grid 7-kolom dan 5-kolom yang rapi dan elegan pada desktop.
