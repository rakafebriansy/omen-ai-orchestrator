---
id: TICKET-90
title: Pembuatan API Route Feed Aktivitas Publik On-Chain (GET /api/activity)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/app/api/activity/route.ts` untuk `GET /api/activity`.
- [ ] Mengagregasikan peristiwa aktivitas secara terurut descending berdasarkan timestamp `created_at`.
- [ ] Melakukan join dengan tabel `beliefs` dan `markets` untuk menyediakan teks ringkasan konteks pasar.
- [ ] Mendukung query pagination dan filter berdasarkan `market_id` tertentu.
- [ ] Menyusun unit test pada `omen/web/tests/api-activity.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/activity/route.ts`
- `omen/web/tests/api-activity.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
