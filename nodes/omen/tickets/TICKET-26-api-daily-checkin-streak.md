---
id: TICKET-26
title: Pembuatan API Route Daily Check-in Streak
status: Todo
priority: Medium
labels: [Backend, API, Gamification]
---

# Deskripsi
Mengembangkan API endpoint POST /api/checkin untuk memvalidasi interval 24 jam, menambah streak, dan mencatat poin reward.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menolak check-in ganda dalam durasi kurang dari 24 jam.
- [ ] Menambah streak counter jika check-in dalam jendela 24 sampai 48 jam.
- [ ] Mereset streak ke 1 jika interval lebih dari 48 jam dan mencatat ke points_events.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/checkin/route.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
