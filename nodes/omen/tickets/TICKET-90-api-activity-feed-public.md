---
id: TICKET-90
title: Pembuatan API Route Feed Aktivitas Publik On-Chain (GET /api/activity)
status: Done
priority: Medium
labels: [Backend, API, Activity, Supabase]
---

# Deskripsi
Tiket ini menyediakan endpoint serverless `GET /api/activity` yang menyatukan peristiwa-peristiwa penting dalam ekosistem OMEN menjadi feed kronologis publik terpadu.

Sumber peristiwa yang digabungkan:
- Penempatan posisi keyakinan baru (`market_positions` -> "AGREED / DISAGREED").
- Konfirmasi resmi kreator (`creator_confirmations` -> "CONFIRMED BELIEF").
- Resolusi pasar (`market_resolutions` -> "RESOLVED").
- Klaim kemenangan pengguna (`market_events` type `PayoutClaimed` -> "CLAIMED PAYOUT").

Query mendukung filter `market_id` opsional, limit (default 20, max 100), cursor pagination, serta join ke metadata tabel `beliefs` untuk menyajikan ringkasan teks keyakinan dan author terkait.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/app/api/activity/route.ts` untuk `GET /api/activity`.
- [x] Mengagregasikan peristiwa aktivitas secara terurut descending berdasarkan timestamp `created_at`.
- [x] Melakukan join dengan tabel `beliefs` dan `markets` untuk menyediakan teks ringkasan konteks pasar.
- [x] Mendukung query pagination dan filter berdasarkan `market_id` tertentu.
- [x] Menyusun unit test pada `omen/web/tests/api-activity.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/activity/route.ts`
- `omen/web/tests/api-activity.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/api-activity.test.ts` yang memverifikasi kepatuhan Zero-Comment Policy, pengambilan feed kronologis terpadu dengan relasi pasar & keyakinan, filter `market_id` dan `event_type`, serta penanganan HTTP 500 error database.
  2. Mengembangkan route handler `GET /api/activity` pada `omen/web/app/api/activity/route.ts` dengan join relasional Supabase ke `markets` dan `beliefs`, sorting descending berdasarkan `created_at`, serta pagination range.
  3. Memvalidasi seluruh test vitest, typecheck tsc, dan linting ESLint tanpa error maupun auto-fix.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/activity/route.ts`
  - `omen/web/tests/api-activity.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggabungkan data event secara flat (`statement`, `belief_author`, `market_contract_address`, `market_chain_id`) untuk kemudahan konsumsi komponen UI Activity Feed di frontend.
