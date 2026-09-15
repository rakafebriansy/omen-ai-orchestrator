---
id: TICKET-19
title: Pembuatan Form Admin Pembuatan Pasar Prediksi
status: Todo
priority: Medium
labels: [Frontend, Admin, UI]
---

# Deskripsi
Membangun formulir antarmuka admin `AdminMarketCreateForm` di `omen/web/components/AdminMarketCreateForm.tsx` untuk mendaftarkan pasar prediksi baru beserta live preview kartu pasar.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`AdminMarketCreateForm.tsx`)
1. **Tata Letak Formulir (Form Grid):**
   - `bg-white border border-border-subtle rounded-2xl p-6 sm:p-8 shadow-sm space-y-6`.
2. **Field Masukan (Input Fields):**
   - Field Judul Prediksi: Input teks `border border-border-subtle rounded-lg p-3 w-full font-medium` (contoh: "Will ETH cross $4,000 by end of month?").
   - Field Kategori: Dropdown select (Crypto, Meme, Narratives, Trending).
   - Field Deadline: Date dan Time picker dengan validasi minimal 1 jam di masa depan.
   - Field Sumber Resolusi: Input URL referensi sumber berita / indexer harga.
3. **Live Card Preview:**
   - Panel samping yang menampilkan simulasi visual `MarketCard` secara instan sesuai data yang sedang diketik.
4. **Tombol Submit:**
   - "Publish Market to Blockchain" (`bg-primary-blue text-white py-3 px-6 rounded-lg font-bold`).

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Formulir memvalidasi seluruh input wajib dan batas waktu minimal 1 jam di masa depan.
- [ ] Live preview merender kartu pasar secara interaktif.
- [ ] Unit test komponen AdminMarketCreateForm lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketCreateForm.tsx`
- `omen/web/tests/admin-create-form.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
