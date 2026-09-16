---
id: TICKET-21
title: Pembuatan Interface Admin Resolusi Pasar Prediksi
status: Done
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
- [x] Tabel hanya menampilkan pasar yang sudah melewati batas waktu deadline.
- [x] Tombol resolusi memicu modal konfirmasi ganda sebelum eksekusi.
- [x] Unit test komponen AdminMarketResolutionTable lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketResolutionTable.tsx`
- `omen/web/tests/admin-resolution-table.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan komponen antarmuka admin `AdminMarketResolutionTable.tsx` dengan daftar pasar expired pending resolution, tombol aksi resolusi "Resolve YES", "Resolve NO", dan "Cancel & Refund", serta modal dialog konfirmasi ganda (*Double Confirmation Modal*) dengan validasi checkbox verifikasi oracle, warning irreversible on-chain settlement, dan form input catatan resolusi.
  2. Mengimplementasikan test suite lengkap di `omen/web/tests/admin-resolution-table.test.tsx` (6 pengujian mencakup rendering baris pasar dan tombol aksi, search filter pasar, pemicuan dialog konfirmasi ganda, validasi proteksi checkbox bukti oracle, eksekusi settlement sukses dengan callback `onResolveMarket`, dan penutupan dialog saat batal).
  3. Memvalidasi eksekusi seluruh pengujian dengan Vitest (107/107 test passed 100%) dan verifikasi type check TypeScript (`tsc --noEmit`).
  4. Memverifikasi kepatuhan terhadap Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/AdminMarketResolutionTable.tsx`
  - `omen/web/tests/admin-resolution-table.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menerapkan mekanisme proteksi modal konfirmasi ganda (*double confirmation*) untuk memitigasi kesalahan manusia dalam penyelesaian on-chain prediction market payouts.
