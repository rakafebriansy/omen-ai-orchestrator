---
id: TICKET-65
title: (MANUAL) Migrasi Skema Basis Data Supabase V1 (11 Tabel Arsitektur Social Beliefs)
status: Done
priority: High
labels: [Backend, Database, Supabase, Migration, ManualAction]
---

# Deskripsi
Arsitektur OMEN V1 bertransformasi dari pasar prediksi biner biasa menjadi protokol Social Belief Market yang berpusat pada entitas Belief dan Kreator. Skema database existing (5 tabel) perlu dimutakhirkan melalui skrip migrasi additive `02_v1_belief_schema.sql` untuk mendukung 11 tabel inti V1:
1. `beliefs`
2. `belief_sources`
3. `markets` (v1)
4. `market_positions`
5. `market_events`
6. `market_resolutions`
7. `market_settlements`
8. `creator_profiles`
9. `creator_confirmations`
10. `oracle_snapshots`
11. `users` (v1)

Tiket ini mencakup pembuatan file DDL migrasi SQL oleh AI, eksekusi manual skrip SQL pada Supabase Dashboard / SQL Editor oleh Developer, serta sinkronisasi tipe TypeScript pada `types/database.ts`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] AI Agent menyusun skrip DDL migrasi SQL `omen/web/db/migrations/02_v1_belief_schema.sql` (11 tabel, foreign keys, constraints, dan performance indexes).
- [x] AI Agent menyusun skrip rollback `omen/web/db/migrations/02_v1_belief_rollback.sql`.
- [x] **(Manual Developer)** Developer mengeksekusi script SQL migrasi `02_v1_belief_schema.sql` pada SQL Editor Supabase Cloud / Local.
- [x] **(Manual Developer)** Developer memverifikasi 11 tabel dan RLS policies terbuat dengan benar di Supabase Table Editor.
- [x] AI Agent memperbarui `omen/web/types/database.ts` dengan type definitions TypeScript yang presisi untuk seluruh entitas V1.
- [x] Menyusun unit test validasi skema database di `omen/web/tests/api-schema-v1.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/db/migrations/02_v1_belief_schema.sql`
- `omen/web/db/migrations/02_v1_belief_rollback.sql`
- `omen/web/types/database.ts`
- `omen/web/tests/api-schema-v1.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis test TDD di `omen/web/tests/api-schema-v1.test.ts` untuk memvalidasi keberadaan DDL, kepatuhan Zero-Comment, 11 tabel inti, tipe `TIMESTAMPTZ`, foreign key, check constraints, performa index, RLS policies, dan tipe TypeScript.
  2. Menyusun file DDL migrasi additive `omen/web/db/migrations/02_v1_belief_schema.sql` yang mendefinisikan 11 entitas (`beliefs`, `belief_sources`, `markets`, `market_positions`, `market_events`, `market_resolutions`, `market_settlements`, `creator_profiles`, `creator_confirmations`, `oracle_snapshots`, `users`) dengan indeks dan RLS.
  3. Menyusun file rollback `omen/web/db/migrations/02_v1_belief_rollback.sql`.
  4. Memperbarui definisi tipe TypeScript pada `omen/web/types/database.ts` dengan interface lengkap 11 tabel V1 dan relasinya.
  5. Menjalankan test suite Vitest: seluruh 9 test `api-schema-v1.test.ts` dan 258 total test aplikasi lulus 100%.
  6. Memverifikasi type-checking dengan `npx tsc --noEmit` dan linter `npx eslint` dengan 0 error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/db/migrations/02_v1_belief_schema.sql` (Skrip DDL migrasi 11 tabel V1, indeks, dan RLS)
  - `omen/web/db/migrations/02_v1_belief_rollback.sql` (Skrip DDL rollback migrasi V1)
  - `omen/web/types/database.ts` (Type definitions TypeScript untuk 11 entitas basis data)
  - `omen/web/tests/api-schema-v1.test.ts` (Unit test validasi skema DDL & TypeScript)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Seluruh timestamp menggunakan `TIMESTAMPTZ` untuk menghindari mismatch timezone antar zona waktu global.
  - Skrip migrasi dirancang additive dengan blok `DO $$` untuk menambahkan kolom-kolom baru pada tabel `markets` tanpa merusak backward-compatibility data pasar eksisting.
  - Zero-Comment Policy ditegakkan secara ketat pada seluruh file `.sql` dan `.ts` yang dibuat.
