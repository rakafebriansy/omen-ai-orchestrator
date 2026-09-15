---
id: TICKET-28
title: Pembuatan API Route Verifikasi Quest
status: Todo
priority: Medium
labels: [Backend, API, Gamification]
---

# Deskripsi
Mengembangkan API endpoint POST /api/quests/[id]/complete untuk memvalidasi pemenuhan syarat misi dan mengalokasikan poin reward.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memvalidasi keabsahan quest_id dan mencegah klaim ganda.
- [ ] Menambah saldo total_points di tabel users.
- [ ] Menyimpan audit trail transaksi ke tabel points_events.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/quests/[id]/complete/route.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
