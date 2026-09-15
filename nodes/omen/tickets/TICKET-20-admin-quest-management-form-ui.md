---
id: TICKET-20
title: Pembuatan Form Admin Manajemen Quest
status: Todo
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
- [ ] Formulir mengizinkan input quest baru dengan validasi nilai poin positif.
- [ ] Tabel daftar quest menampilkan toggle status aktif/nonaktif.
- [ ] Unit test komponen AdminQuestManagementForm lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminQuestManagementForm.tsx`
- `omen/web/tests/admin-quest-form.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
