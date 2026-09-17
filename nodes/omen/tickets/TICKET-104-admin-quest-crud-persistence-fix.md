---
id: TICKET-104
title: Fix Admin Quest CRUD Database Persistence (Create, Toggle, Delete)
status: Done
priority: High
labels: [Frontend, Backend, Bug, Supabase, Quests]
---

# Deskripsi
Perbaikan persistensi data pada modul manajemen quest di dashboard admin (`/admin`). Sebelumnya, pembuatan quest dan pengalihan status aktif (toggle) hanya memodifikasi local state React karena adanya conditional branch `if (onCreateQuest)` dan `if (onToggleQuestStatus)` yang membajak pemanggilan API `/api/admin/quests`. Hal ini menyebabkan data quest yang dibuat hilang setelah halaman di-refresh dan quest baru menggunakan ID sementara (`quest-${Date.now()}`) bukan ID UUID dari Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `AdminQuestManagementForm.tsx` selalu mengirimkan permintaan HTTP `POST /api/admin/quests` secara langsung tanpa diblokir oleh callback `onCreateQuest`.
- [x] ID quest baru menggunakan UUID resmi dari response Supabase (`/api/admin/quests`).
- [x] Pengalihan status quest (toggle active/inactive) selalu mengirimkan permintaan HTTP `PATCH /api/admin/quests/[id]` sebelum memutakhirkan state lokal.
- [x] Penghapusan quest (delete) memverifikasi `response.ok` dari `DELETE /api/admin/quests/[id]` sebelum memperbarui state tampilan.
- [x] Daftar quest pada `AdminQuestManagementForm` tersinkronisasi dengan pembaruan prop `initialQuests` dari parent `AdminDashboardPage`.
- [x] Alamat hardcoded dummy admin dihapus dari `AUTHORIZED_ADMIN_ADDRESSES` pada `web/app/admin/page.tsx`.

## Target Lingkup File (Affected Files)
- `web/components/AdminQuestManagementForm.tsx`
- `web/app/admin/page.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengeliminasi conditional branching `if (onCreateQuest) / else` pada `handleCreateSubmit` di `AdminQuestManagementForm.tsx`.
  2. Mengimplementasikan fetch langsung ke `POST /api/admin/quests`, memvalidasi respon status `201`, dan mengambil objek quest tersimpan dari Supabase.
  3. Mengeliminasi conditional branching `if (onToggleQuestStatus) / else` pada `handleToggle` di `AdminQuestManagementForm.tsx`.
  4. Mengimplementasikan fetch langsung ke `PATCH /api/admin/quests/${id}` dengan verifikasi `response.ok`.
  5. Memperketat `handleConfirmDelete` untuk memeriksa `response.ok` dari `DELETE /api/admin/quests/${id}`.
  6. Menambahkan `useEffect` sinkronisasi `initialQuests` pada `AdminQuestManagementForm.tsx`.
  7. Menghapus dummy addresses `"0x1234567890abcdef..."` dan `"0xAdmin999..."` dari `AUTHORIZED_ADMIN_ADDRESSES` di `web/app/admin/page.tsx`.
- **Ringkasan File Terpengaruh:**
  - `web/components/AdminQuestManagementForm.tsx`
  - `web/app/admin/page.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Callback parent `onCreateQuest`, `onToggleQuestStatus`, dan `onDeleteQuest` tetap dipanggil setelah request API berhasil guna menyinkronkan metrik agregat di level `AdminDashboardPage`.
