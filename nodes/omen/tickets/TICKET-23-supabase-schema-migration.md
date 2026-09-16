---
id: TICKET-23
title: Skema Basis Data Supabase Migration
status: Done
priority: High
labels: [Backend, Database]
---

# Deskripsi
Membuat berkas migrasi SQL lengkap di `omen/web/db/migrations/01_init_schema.sql` untuk menginisialisasi skema basis data PostgreSQL Supabase sesuai spesifikasi System Design.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Skema Tabel SQL
1. **Tabel `users`:**
   - `id UUID PRIMARY KEY DEFAULT gen_random_uuid()`
   - `wallet_address TEXT UNIQUE NOT NULL`
   - `total_points NUMERIC NOT NULL DEFAULT 0`
   - `last_checkin_at TIMESTAMPTZ`
   - `streak_count INTEGER NOT NULL DEFAULT 0`
   - `created_at TIMESTAMPTZ NOT NULL DEFAULT now()`
2. **Tabel `quests`:**
   - `id UUID PRIMARY KEY DEFAULT gen_random_uuid()`
   - `title TEXT NOT NULL`
   - `description TEXT`
   - `points_reward NUMERIC NOT NULL`
   - `is_active BOOLEAN NOT NULL DEFAULT true`
   - `created_at TIMESTAMPTZ NOT NULL DEFAULT now()`
3. **Tabel `points_events`:**
   - `id UUID PRIMARY KEY DEFAULT gen_random_uuid()`
   - `wallet_address TEXT NOT NULL`
   - `quest_id UUID REFERENCES quests(id)`
   - `source TEXT NOT NULL CHECK (source IN ('daily_checkin', 'quest', 'prediction_market', 'referral'))`
   - `points NUMERIC NOT NULL`
   - `created_at TIMESTAMPTZ NOT NULL DEFAULT now()`
4. **Tabel `markets`:**
   - `id UUID PRIMARY KEY DEFAULT gen_random_uuid()`
   - `contract_market_id INTEGER UNIQUE NOT NULL`
   - `title TEXT NOT NULL`
   - `description TEXT`
   - `deadline TIMESTAMPTZ NOT NULL`
   - `status TEXT NOT NULL DEFAULT 'active' CHECK (status IN ('active', 'resolved_yes', 'resolved_no', 'cancelled'))`
   - `total_pool_yes NUMERIC NOT NULL DEFAULT 0`
   - `total_pool_no NUMERIC NOT NULL DEFAULT 0`
   - `resolution_source TEXT`
   - `created_at TIMESTAMPTZ NOT NULL DEFAULT now()`
5. **Tabel `bets`:**
   - `id UUID PRIMARY KEY DEFAULT gen_random_uuid()`
   - `market_id UUID REFERENCES markets(id) NOT NULL`
   - `wallet_address TEXT NOT NULL`
   - `side TEXT NOT NULL CHECK (side IN ('yes', 'no'))`
   - `amount NUMERIC NOT NULL`
   - `claimed BOOLEAN NOT NULL DEFAULT false`
   - `tx_hash TEXT UNIQUE NOT NULL`
   - `created_at TIMESTAMPTZ NOT NULL DEFAULT now()`

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Seluruh 5 tabel utama terdefinisi lengkap dengan constraints, default values, dan foreign keys.
- [x] Semua kolom waktu menggunakan tipe data TIMESTAMPTZ sesuai pedoman database.
- [x] Indeks performa dibuat untuk kolom query kritis (wallet_address, contract_market_id, status).

## Target Lingkup File (Affected Files)
- `omen/web/db/migrations/01_init_schema.sql`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Merancang dan menulis berkas migrasi SQL `omen/web/db/migrations/01_init_schema.sql` yang mendefinisikan 5 tabel utama (`users`, `quests`, `points_events`, `markets`, `bets`), ekstensi `pgcrypto`, relasi Foreign Keys, default values (`gen_random_uuid()`, `now()`), Check constraints domain, serta 10 indeks performa.
  2. Mematuhi Zero-Comment Policy secara mutlak dengan memastikan tidak ada komentar SQL (`--` atau `/* */`) pada berkas migrasi.
  3. Memastikan semua kolom datetime (`created_at`, `deadline`, `last_checkin_at`) menggunakan tipe data `TIMESTAMPTZ` (UTC netral waktu) sesuai pedoman arsitektur basis data.
  4. Menulis unit test integritas skema dan validasi Zero-Comment Policy di `omen/web/tests/api-schema.test.ts`.
  5. Memvalidasi eksekusi pengujian `npm run test` (23 test files, 135 tests pass 100%) dan verifikasi type checking `npx tsc --noEmit` bersih tanpa error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/db/migrations/01_init_schema.sql` (Created)
  - `omen/web/tests/api-schema.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-23-supabase-schema-migration.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Tipe data waktu menggunakan `TIMESTAMPTZ` untuk mematuhi Opsi 2 pada `global-guidelines/database.md`.
  - Indeks performa dibuat tidak hanya untuk kueri kritis utama (`wallet_address`, `contract_market_id`, `status`), melainkan juga untuk `total_points DESC` guna mengoptimalkan query leaderboard TICKET-29.
