---
id: TICKET-21
title: Pembuatan Interface Admin Resolusi Pasar Prediksi
status: Todo
priority: Medium
labels: [Frontend, Admin, UI]
---

# Deskripsi
Membangun antarmuka admin `AdminMarketResolutionTable` di `omen/web/components/AdminMarketResolutionTable.tsx` yang menyajikan daftar pasar yang telah melewati batas deadline untuk di-resolve hasilnya (Yes/No/Cancel).

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`AdminMarketResolutionTable.tsx`)
1. **Daftar Pasar Expired:**
   - Tabel memuat daftar pasar dengan status aktif yang batas waktunya sudah lewat (`deadline < now`).
2. **Kontrol Resolusi per Baris:**
   - Tombol "Resolve YES" (Hijau).
   - Tombol "Resolve NO" (Merah).
   - Tombol "Cancel dan Refund" (Abu-abu / Peringatan).
3. **Dialog Konfirmasi Ganda:**
   - Pop-up konfirmasi wajib sebelum transaksi on-chain dikirim, meminta admin memverifikasi sumber bukti.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Tabel hanya menampilkan pasar yang sudah melewati batas waktu deadline.
- [ ] Tombol resolusi memicu modal konfirmasi ganda sebelum eksekusi.
- [ ] Unit test komponen AdminMarketResolutionTable lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketResolutionTable.tsx`
- `omen/web/tests/admin-resolution-table.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
