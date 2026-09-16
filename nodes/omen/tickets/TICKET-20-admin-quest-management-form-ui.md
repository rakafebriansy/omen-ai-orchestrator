---
id: TICKET-20
title: Pembuatan Form Admin Manajemen Quest
status: Done
priority: Medium
labels: [Frontend, Admin, UI]
---

# Deskripsi
Membangun formulir antarmuka admin `AdminQuestManagementForm` di `omen/web/components/AdminQuestManagementForm.tsx` untuk menambah quest baru dan mengatur toggle aktif/nonaktif daftar quest eksisting.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`AdminQuestManagementForm.tsx`)
1. **Formulir Tambah Quest:**
   - Input judul tugas, deskripsi instruksi, reward poin, dan kategori tugas.
   - Tombol submit "Create Quest".
2. **Tabel Manajemen Quest Eksisting:**
   - Daftar tabel memuat ID quest, judul, reward poin, dan switch toggle aktif/nonaktif.
   - Toggle switch interaktif dengan konfirmasi visual status perubahan.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Formulir mengizinkan input quest baru dengan validasi nilai poin positif.
- [x] Tabel daftar quest menampilkan toggle status aktif/nonaktif.
- [x] Unit test komponen AdminQuestManagementForm lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminQuestManagementForm.tsx`
- `omen/web/tests/admin-quest-form.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan komponen `AdminQuestManagementForm.tsx` yang mencakup form pendaftaran quest baru dengan validasi poin positif, kategori, deskripsi, URL aksi opsional, serta tabel manajemen quest dengan toggle switch interaktif aktif/nonaktif.
  2. Mengimplementasikan test suite lengkap di `omen/web/tests/admin-quest-form.test.tsx` (7 pengujian mencakup rendering, validasi input, callback submit `onCreateQuest`, toggle status aktif/nonaktif `onToggleQuestStatus`, search filter, dan active/inactive tab filtering).
  3. Memvalidasi eksekusi seluruh pengujian dengan Vitest (101/101 test passed) dan memastikan tidak ada error TypeScript (`tsc --noEmit`).
  4. Memverifikasi kepatuhan terhadap Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/AdminQuestManagementForm.tsx`
  - `omen/web/tests/admin-quest-form.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengintegrasikan state management lokal dan callback props asynchronous untuk memastikan fleksibilitas integrasi dengan API backend (TICKET-30/TICKET-31) dan transaksi smart contract.
