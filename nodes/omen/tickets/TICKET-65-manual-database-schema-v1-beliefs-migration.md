---
id: TICKET-65
title: (MANUAL) Migrasi Skema Basis Data Supabase V1 (11 Tabel Arsitektur Social Beliefs)
status: Todo
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
- [ ] AI Agent menyusun skrip DDL migrasi SQL `omen/web/db/migrations/02_v1_belief_schema.sql` (11 tabel, foreign keys, constraints, dan performance indexes).
- [ ] AI Agent menyusun skrip rollback `omen/web/db/migrations/02_v1_belief_rollback.sql`.
- [ ] **(Manual Developer)** Developer mengeksekusi script SQL migrasi `02_v1_belief_schema.sql` pada SQL Editor Supabase Cloud / Local.
- [ ] **(Manual Developer)** Developer memverifikasi 11 tabel dan RLS policies terbuat dengan benar di Supabase Table Editor.
- [ ] AI Agent memperbarui `omen/web/types/database.ts` dengan type definitions TypeScript yang presisi untuk seluruh entitas V1.
- [ ] Menyusun unit test validasi skema database di `omen/web/tests/api-schema-v1.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/db/migrations/02_v1_belief_schema.sql`
- `omen/web/db/migrations/02_v1_belief_rollback.sql`
- `omen/web/types/database.ts`
- `omen/web/tests/api-schema-v1.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
