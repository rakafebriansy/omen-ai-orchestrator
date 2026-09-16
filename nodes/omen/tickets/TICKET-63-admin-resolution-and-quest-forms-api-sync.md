---
id: TICKET-63
title: Integrasi Live API Data pada Admin Market Resolution Table & Quest Management Form
status: Done
priority: Medium
labels: [Frontend, Backend, Admin, Supabase, SmartContract]
---

# Deskripsi
Komponen admin `components/AdminMarketResolutionTable.tsx` dan `components/AdminQuestManagementForm.tsx` masih memuat daftar statis `DEFAULT_RESOLVABLE_MARKETS` (baris 71–110) dan `DEFAULT_QUESTS` (baris 31–92, disertai komentar TODO(TICKET-53)). Selain itu, props default ini berpotensi menimpa atau menyamarkan status data pasar dan quest sebenarnya di database.

Tiket ini bertujuan untuk menghapus dataset tiruan `DEFAULT_RESOLVABLE_MARKETS` dan `DEFAULT_QUESTS`, memastikan form dan tabel admin diinisialisasi dengan data dinamis dari `GET /api/markets` dan `GET /api/admin/quests`, serta memverifikasi bahwa mutasi resolusi pasar, pembuatan quest, toggle status, dan penghapusan quest bekerja secara live dan real-time terhadap database Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menghapus array statis `DEFAULT_RESOLVABLE_MARKETS` pada `omen/web/components/AdminMarketResolutionTable.tsx`.
- [x] Menghapus array statis `DEFAULT_QUESTS` dan komentar TODO pada `omen/web/components/AdminQuestManagementForm.tsx`.
- [x] Menghubungkan halaman `omen/web/app/admin/page.tsx` untuk menyuplai daftar pasar yang dapat diselesaikan (resolvable) dan daftar quest admin langsung dari backend API.
- [x] Menyediakan *empty state* yang jelas jika tidak ada pasar yang menunggu resolusi atau belum ada quest yang dibuat.
- [x] Memastikan mutasi resolusi pasar (`useAdminResolveMarket`), pembuatan quest, perubahan status aktif/non-aktif, dan penghapusan quest tersinkronisasi langsung ke Supabase.
- [x] Seluruh unit tests Vitest di `omen/web` lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketResolutionTable.tsx`
- `omen/web/components/AdminQuestManagementForm.tsx`
- `omen/web/app/admin/page.tsx`
- `omen/web/tests/admin-page.test.tsx`
- `omen/web/tests/admin-quest-form.test.tsx`
- `omen/web/tests/admin-resolution-table.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menghapus dataset tiruan `DEFAULT_RESOLVABLE_MARKETS` dari `components/AdminMarketResolutionTable.tsx` dan menggantinya dengan empty array default serta empty state yang informatif.
  2. Menghapus dataset tiruan `DEFAULT_QUESTS` dan komentar TODO(TICKET-53) dari `components/AdminQuestManagementForm.tsx`.
  3. Memperbarui `app/admin/page.tsx` untuk menyuplai daftar pasar resolvable dinamis (`markets.filter(m => m.status === 'open' || m.status === 'closed')`) dan daftar quest admin dari state/API ke masing-masing komponen anak.
  4. Menjalankan seluruh test suite admin (`tests/admin-*.test.tsx`) dan memastikan 36/36 tests lulus.
  5. Memvalidasi seluruh test suite aplikasi (249 tests lulus) dan TypeScript compilation (`npx tsc --noEmit`).
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/AdminMarketResolutionTable.tsx`
  - `omen/web/components/AdminQuestManagementForm.tsx`
  - `omen/web/app/admin/page.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengisolasi state manajemen admin di level `app/admin/page.tsx` yang meneruskan data live dan handler callbacks ke sub-komponen, menjamin keseragaman UI dan revalidasi instan setelah tindakan resolusi atau mutasi quest.
  - Zero-Comment Policy diterapkan 100% pada semua komponen admin.
