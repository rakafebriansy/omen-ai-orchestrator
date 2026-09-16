---
id: TICKET-65
title: Migrasi Skema Basis Data Supabase V1 (11 Tabel Arsitektur Social Beliefs)
status: Todo
priority: High
labels: [Backend, Database, Supabase, Migration]
---

# Deskripsi
Arsitektur OMEN V1 bertransformasi dari sekadar pasar prediksi biner biasa menjadi protokol Social Belief Market yang berpusat pada entitas Belief dan Kreator. Skema database existing (5 tabel: `users`, `quests`, `points_events`, `markets`, `bets`) perlu dimutakhirkan melalui skrip migrasi additive `02_v1_belief_schema.sql` untuk mendukung 11 tabel inti V1:
1. `beliefs` (id, creator_id, raw_statement, structured_data, status: DETECTED/CONFIRMED/CLOSED/RESOLVED, created_at)
2. `belief_sources` (id, belief_id, platform, source_url, author_handle, author_address, timestamp)
3. `markets` (v1: id, belief_id, contract_address, chain_id, status: OPEN/CLOSED/RESOLVED/SETTLED/VOID, agree_pool, disagree_pool, agree_count, disagree_count, open_time, close_time, resolution_type, resolution_config)
4. `market_positions` (id, market_id, wallet_address, side: AGREE/DISAGREE, amount_eth, tx_hash, created_at)
5. `market_events` (id, market_id, event_type, payload, tx_hash, block_number, created_at)
6. `market_resolutions` (id, market_id, outcome: AGREE_WON/DISAGREE_WON/VOID, resolution_price_start, resolution_price_end, oracle_source, resolved_by, tx_hash, resolved_at)
7. `market_settlements` (id, market_id, total_pool, winning_pool, total_payout_claimed, created_at)
8. `creator_profiles` (id, address, handle, avatar_url, total_beliefs, confirmed_beliefs, resolved_beliefs, correct_beliefs, accuracy_rate, total_volume_eth, created_at)
9. `creator_confirmations` (id, belief_id, creator_address, signature, chain_id, confirmed_at)
10. `oracle_snapshots` (id, market_id, asset_symbol, price_usd, snapshot_type: START/END/DISPLAY, source, recorded_at)
11. `users` (v1: id, wallet_address, username, total_volume_eth, total_positions, created_at)

Tiket ini juga mencakup sinkronisasi tipe TypeScript pada `types/database.ts` agar PostgREST query memiliki type-safety penuh.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyusun skrip migrasi SQL `omen/web/db/migrations/02_v1_belief_schema.sql` dengan DDL 11 tabel, foreign key constraints, default value, dan performance indexes.
- [ ] Menerapkan Row Level Security (RLS) policies pada tabel baru (read publik, write terproteksi service role / authenticated wallet).
- [ ] Menyusun skrip rollback `omen/web/db/migrations/02_v1_belief_rollback.sql`.
- [ ] Memperbarui `omen/web/types/database.ts` dengan type definitions TypeScript yang presisi untuk seluruh entitas V1.
- [ ] Menyusun unit test validasi skema database di `omen/web/tests/api-schema-v1.test.ts` dan memastikan seluruh pengujian lulus 100% dengan Zero-Comment Policy.

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
