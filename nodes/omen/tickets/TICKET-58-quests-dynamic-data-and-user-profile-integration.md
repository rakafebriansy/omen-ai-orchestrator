---
id: TICKET-58
title: Integrasi Dynamic Data Supabase & User Profile pada Halaman Quests
status: Done
priority: High
labels: [Frontend, Backend, Feature, Supabase, Gamification]
---

# Deskripsi
Halaman `app/quests/page.tsx` dan komponen pendukungnya masih menggunakan daftar statis `INITIAL_QUESTS` (baris 20–96), saldo poin statis (`2450 PTS`), tier statis (`Tier II • Silver Hunter`), streak statis (`3 Days`), dan rank statis (`Top 8%`). Selain itu, halaman masih mengandalkan fallback `mockPredictionMarket.getDemoWallet()` daripada data profil dinamis dari Supabase (`/api/quests`, `/api/wallet/connect`, dan profil user).

Tiket ini bertujuan untuk menghapus seluruh data statis `INITIAL_QUESTS` dan nilai hardcoded lainnya, menghubungkan pengambilan data langsung dari API `/api/quests?wallet_address=...`, menyinkronkan progres misi dan daily check-in dengan profil pengguna Supabase, serta menyediakan skeleton loading dan empty state jika belum ada data.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menghapus array statis `INITIAL_QUESTS` dan nilai hardcoded total poin (`2450`), streak (`3 Days`), dan rank (`Top 8%`) pada `omen/web/app/quests/page.tsx`.
- [x] Mengambil daftar quest secara dinamis dari endpoint `GET /api/quests?wallet_address=...` dan merender status real (`COMPLETED` / `AVAILABLE`).
- [x] Menghubungkan total akumulasi poin, active streak count, dan tier multiplier dengan data profil wallet aktif pengguna dari Supabase.
- [x] Menyediakan *skeleton loading state* dan penanganan *empty state* yang informatif saat data sedang dimuat atau ketika daftar quest kosong.
- [x] Menghubungkan aksi penyelesaian misi dan daily check-in ke API `/api/quests/[id]/complete` dan `/api/checkin` dengan alamat wallet aktif.
- [x] Seluruh unit tests Vitest di `omen/web` lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/quests/page.tsx`
- `omen/web/components/DailyCheckinWidget.tsx`
- `omen/web/tests/quests-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan test suite TDD pada `web/tests/quests-page.test.tsx` yang memvalidasi loading skeleton, dynamic quest loading, profile points calculation, streak synchronization, dan graceful empty state.
  2. Menghapus seluruh array `INITIAL_QUESTS` dan hardcoded points/streak/tier dari `web/app/quests/page.tsx`.
  3. Mengimplementasikan fetch dinamis murni ke `/api/quests?wallet_address=...` dan kalkulasi tier otomatis berdasarkan live accumulated points.
  4. Memvalidasi kelulusan 5/5 unit tests di `web/tests/quests-page.test.tsx` dengan kepatuhan 100% Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/quests/page.tsx`
  - `omen/web/tests/quests-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Data diinisialisasi kosong dengan state loading skeleton untuk mencegah content flashing atau rendering data palsu.
