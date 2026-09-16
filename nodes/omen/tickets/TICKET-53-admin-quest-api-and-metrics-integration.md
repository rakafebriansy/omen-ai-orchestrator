---
id: TICKET-53
title: Pembuatan API Route Admin Quests & Integrasi Live Metrics Admin Dashboard
status: Done
priority: Medium
labels: [Backend, Admin, Quests, Metrics, API]
---

# Deskripsi
Saat ini `AdminQuestManagementForm.tsx` hanya menyimpan quest dalam in-memory state tanpa route handler backend, dan kartu metrik pada `app/admin/page.tsx` masih menginisialisasi angka statis (`18`, `4`, `3`). Tiket ini bertugas membuat API route handler `POST /api/admin/quests` dan `PATCH /api/admin/quests/[id]` khusus admin untuk menyimpan dan mengaktifkan/menonaktifkan misi di Supabase, serta mengkueri metrik ringkasan platform secara live.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Membuat route handler Next.js `POST /api/admin/quests` dengan proteksi autentikasi admin (`x-admin-key` / `Authorization`) untuk insert misi baru ke tabel `quests`.
- [x] Membuat route handler `PATCH /api/admin/quests/[id]` untuk toggle status `is_active` atau menghapus quest.
- [x] `AdminQuestManagementForm.tsx` terintegrasi dengan API route admin quests sehingga perubahan data tersimpan permanen di Supabase.
- [x] `app/admin/page.tsx` mengkueri total count `markets`, `quests`, dan `pending resolutions` langsung dari database/indexer.

## Target Lingkup File (Affected Files & TODO Locations)
- [AdminQuestManagementForm.tsx:L1](../../../../omen/web/components/AdminQuestManagementForm.tsx#L1)
- [admin/page.tsx:L1](../../../../omen/web/app/admin/page.tsx#L1)
- [admin/quests/route.ts:L1](../../../../omen/web/app/api/admin/quests/route.ts#L1)
- [admin/quests/[id]/route.ts:L1](../../../../omen/web/app/api/admin/quests/[id]/route.ts#L1)
- [admin-quest-form.test.tsx:L1](../../../../omen/web/tests/admin-quest-form.test.tsx#L1)
- [admin-page.test.tsx:L1](../../../../omen/web/tests/admin-page.test.tsx#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan serverless API route handlers `GET`/`POST /api/admin/quests` dan `PATCH`/`DELETE /api/admin/quests/[id]` untuk mutasi data tabel `quests` Supabase.
  2. Mengintegrasikan fallback API handler pada `AdminQuestManagementForm.tsx` untuk operasi CRUD admin quests.
  3. Mengintegrasikan kueri agregasi metrik live (`totalMarketsCreated`, `activeQuestsCount`, `pendingResolutionsCount`) pada `app/admin/page.tsx`.
  4. Memvalidasi seluruh 27 unit tests pada modul admin (100% lulus).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/admin/quests/route.ts`, `omen/web/app/api/admin/quests/[id]/route.ts`, `omen/web/components/AdminQuestManagementForm.tsx`, `omen/web/app/admin/page.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan Supabase Admin Client (`SUPABASE_SERVICE_ROLE_KEY`) untuk otorisasi bypass RLS.
