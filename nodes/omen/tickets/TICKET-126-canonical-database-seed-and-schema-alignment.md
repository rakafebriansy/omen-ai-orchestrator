---
id: TICKET-126
title: Canonical Database Seed and Schema Alignment
status: Done
priority: Medium
labels: [Database, Backend, Schema]
---

# Deskripsi
File inisialisasi basis data `web/db/seed.sql` sebelumnya masih memuat beberapa referensi usang dari skema legacy, seperti kolom lama (`yes_pool`, `no_pool`, `total_pool_yes`, `total_pool_no`), format status huruf kecil, serta data profil kreator yang belum tersinkronisasi dengan relasi keyakinan baru.

Tiket ini melakukan refactoring pada `web/db/seed.sql` untuk menyelaraskan seluruh data awal dengan skema kanonikal `agree_pool`, `disagree_pool`, `total_pool`, Chain ID resmi (`11155111` dan `46630`), status kapital `OPEN`/`RESOLVED`/`VOID`, serta menyertakan profil kreator yang lengkap.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memperbarui seluruh insert query tabel `markets` di `web/db/seed.sql` agar hanya menggunakan kolom kanonikal `agree_pool`, `disagree_pool`, `total_pool`.
- [x] Menghapus kolom deprecated `yes_pool`, `no_pool`, `total_pool_yes`, `total_pool_no` dari seed script.
- [x] Memastikan nilai `chain_id` konsisten dengan `11155111` (Ethereum Sepolia) dan `46630` (Robinhood Chain Testnet).
- [x] Memastikan status pasar menggunakan format standar huruf besar `OPEN`, `RESOLVED`, `VOID`.
- [x] Menyertakan entri `creator_profiles` awal yang lengkap untuk seeding lokal dan lingkungan testing.

## Target Lingkup File (Affected Files)
- `omen/web/db/seed.sql`

---

## AI Execution Log dan Output

- **Langkah Teknis Tereksekusi:**
  1. Memodifikasi file `web/db/seed.sql` untuk menyelaraskan kolom-kolom tabel `markets`, `beliefs`, dan `creator_profiles`.
  2. Mengganti seluruh alias legacy dengan field kanonikal.
  3. Memvalidasi sintaks SQL agar kompatibel dengan PostgreSQL / Supabase CLI.

- **Ringkasan File Terpengaruh:**
  - `omen/web/db/seed.sql`

- **Catatan dan Keputusan Arsitektural:**
  - Standardisasi skema seed memastikan lingkungan pengujian lokal baru akan selalu menghasilkan state data yang identik dengan arsitektur produksi.
