---
id: TICKET-46
title: (MANUAL) Penyediaan Kredensial Supabase & Eksekusi Skema Migrasi Basis Data
status: Done
priority: High
labels: [Database, Backend, ManualAction, Supabase, Setup]
---

# Deskripsi
Platform Omen membutuhkan basis data PostgreSQL Supabase aktif untuk menyimpan data pengguna (`users`), daftar quest (`quests`), audit poin (`points_events`), metadata pasar (`markets`), dan transaksi taruhan (`bets`). Skema migrasi SQL telah tersedia di `omen/web/db/migrations/01_init_schema.sql`, namun memerlukan eksekusi manual pada instance Supabase Cloud / Local milik developer dan pengisian variabel lingkungan pada `.env.local`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Developer membuat project Supabase baru di Supabase Cloud (atau menjalankan Supabase CLI local).
- [x] Developer mengeksekusi script SQL migrasi `omen/web/db/migrations/01_init_schema.sql` pada SQL Editor Supabase.
- [x] Memastikan 5 tabel utama (`users`, `quests`, `points_events`, `markets`, `bets`) serta indeks dan constraints terbuat dengan benar.
- [x] Mengisi variabel lingkungan di `omen/web/.env.local`:
  - `NEXT_PUBLIC_SUPABASE_URL`
  - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
  - `SUPABASE_SERVICE_ROLE_KEY`
- [x] Menjalankan seeding awal data quest default pada tabel `quests`.

## Target Lingkup File (Affected Files)
- `omen/web/.env.local`
- [01_init_schema.sql:L1](../../../../omen/web/db/migrations/01_init_schema.sql#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Developer mengonfigurasi instance Supabase Cloud dan mengisi variabel lingkungan `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, dan `SUPABASE_SERVICE_ROLE_KEY` pada `.env.local`.
  2. Developer mengeksekusi migrasi skema DDL SQL `01_init_schema.sql` yang mendefinisikan 5 tabel (`users`, `quests`, `points_events`, `markets`, `bets`), indeks performa kueri, serta Row Level Security (RLS) policies.
  3. Menyiapkan skrip rollback `01_rollback_schema.sql` untuk keamanan pemulihan basis data.
- **Ringkasan File Terpengaruh:**
  - `omen/web/.env.local`
  - `omen/web/db/migrations/01_init_schema.sql`
  - `omen/web/db/migrations/01_rollback_schema.sql`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - RLS diaktifkan pada semua tabel dengan *Public Read Policy* (`SELECT`) untuk klien publik, dan seluruh mutasi data (*INSERT/UPDATE*) diamankan melalui serverless route handlers dengan `service_role`.
