---
id: TICKET-22
title: Pembuatan Halaman Admin Dashboard
status: Todo
priority: Medium
labels: [Frontend, Admin, UI]
---

# Deskripsi
Membangun halaman terisolasi `/admin` di `omen/web/app/admin/page.tsx` dengan proteksi otorisasi alamat dompet admin dan navigasi tab antar-panel manajemen.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Halaman (`app/admin/page.tsx`)
1. **Pemeriksaan Otorisasi (Admin Gate):**
   - Memvalidasi apakah alamat dompet cocok dengan `NEXT_PUBLIC_ADMIN_WALLET_ADDRESS`.
   - Jika bukan admin: Menampilkan layar penuh "Access Denied — Administrator Wallet Required".
2. **Tab Navigasi Admin:**
   - Tab 1: "Create Prediction Market" (merender `AdminMarketCreateForm`).
   - Tab 2: "Manage Quests" (merender `AdminQuestManagementForm`).
   - Tab 3: "Resolve Expired Markets" (merender `AdminMarketResolutionTable`).

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Layar Access Denied muncul jika dompet bukan admin yang berwenang.
- [ ] Tab navigasi memfasilitasi perpindahan antar-panel manajemen dengan mulus.
- [ ] Unit test halaman admin dashboard berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/admin/page.tsx`
- `omen/web/tests/admin-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
