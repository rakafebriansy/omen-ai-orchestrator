---
id: TICKET-27
title: Pembuatan API Route Daftar Quest
status: Done
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
- [x] Mengembalikan seluruh quest dengan status is_active = true.
- [x] Menyertakan status boolean penyelesaian quest per wallet address.
- [x] Unit test API route quests list lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/quests/route.ts`
- `omen/web/tests/api-quests.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan serverless Next.js API route handler `GET /api/quests` di `omen/web/app/api/quests/route.ts`.
  2. Mengimplementasikan kueri seleksi seluruh quest aktif (`is_active: true`) dari tabel Supabase `quests`.
  3. Mengimplementasikan parsing query param opsional `wallet_address`, verifikasi format EVM regex, serta pencocokan relasi riwayat penyelesaian pada tabel `points_events` (`source = 'quest'`) untuk memetakan status `is_completed: boolean`.
  4. Menulis unit test komprehensif di `omen/web/tests/api-quests.test.ts` (4 skenario uji: kueri publik tanpa wallet, pencocokan flag penyelesaian dengan wallet, penanganan error database 500, dan Zero-Comment Policy).
  5. Memvalidasi seluruh test suite Vitest `npm run test` (27 file, 160 test lolos 100%) dan type check `npx tsc --noEmit` lolos tanpa error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/quests/route.ts` (Created)
  - `omen/web/tests/api-quests.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-27-api-quests-list.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Penyelesaian quest diakumulasikan menggunakan `Set<string>` in-memory untuk efisiensi kompleksitas waktu O(1) saat melakukan mapping respons array.
