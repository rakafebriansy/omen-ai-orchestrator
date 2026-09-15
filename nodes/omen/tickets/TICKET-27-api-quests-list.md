---
id: TICKET-27
title: Pembuatan API Route Daftar Quest
status: Todo
priority: Medium
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `GET /api/quests` di `omen/web/app/api/quests/route.ts` untuk mengembalikan daftar seluruh quest aktif dan status penyelesaian bagi wallet pemanggil.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `GET`
- **Query Params:** `?wallet_address=0x...` (opsional)
- **Response:** Array quest memuat id, title, description, points_reward, dan field boolean `is_completed`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengembalikan seluruh quest dengan status is_active = true.
- [ ] Menyertakan status boolean penyelesaian quest per wallet address.
- [ ] Unit test API route quests list lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/quests/route.ts`
- `omen/web/tests/api-quests.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
