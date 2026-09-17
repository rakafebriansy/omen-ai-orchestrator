---
id: TICKET-109
title: Eliminate API Fallback Operators and Enforce Strict Deterministic Contracts
status: Done
priority: High
labels: [Backend, API, Refactor, ZeroFallbacks, Supabase]
---

# Deskripsi
Mengeliminasi seluruh operator fallback (`||`, `??`), alias multi-key yang ambigu, dan nilai default dummy pada seluruh API Route Handler di `omen/web/app/api`. Menegakkan skema validasi yang ketat dan respons deterministik 100% antara frontend dan backend tanpa toleransi nilai fallback palsu.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Seluruh handler rute di `web/app/api` (`bets/index`, `markets/[id]/position`, `markets/[id]/claim`, `beliefs/submit`, `beliefs/[id]/confirm`, `stats/overview`, `positions`, `markets`, `markets/[id]/resolve`, `oracle/snapshot`, dll.) bebas dari operator fallback `||` dan `??` yang ambigu pada parsing parameter.
- [x] Permintaan dengan parameter yang tidak lengkap, tipe data salah, atau format invalid ditolak langsung dengan status HTTP 400.
- [x] `GET /api/stats/overview` menghitung metrik agregat murni dari database Supabase dan melempar status HTTP 500 jika terjadi kegagalan basis data (menghapus seluruh nilai dummy hardcoded `148.5`, `1420000`, dll.).
- [x] Seluruh hook frontend (`usePlaceBet`, `usePosition`, `useClaim`, `useCreatorConfirm`, `BeliefSubmitForm`) mengirimkan payload dengan nama properti kanonikal yang tepat.
- [x] Seluruh unit test suite Vitest (74 file, 383 unit tests) lulus 100% tanpa kegagalan atau regresi.
- [x] Zero-Comment Policy dipatuhi 100% pada semua file `.ts` dan `.tsx`.

## Target Lingkup File (Affected Files)
- `web/app/api/bets/index/route.ts`
- `web/app/api/markets/[id]/position/route.ts`
- `web/app/api/markets/[id]/claim/route.ts`
- `web/app/api/beliefs/submit/route.ts`
- `web/app/api/beliefs/[id]/confirm/route.ts`
- `web/app/api/stats/overview/route.ts`
- `web/app/api/positions/route.ts`
- `web/app/api/markets/route.ts`
- `web/app/api/markets/[id]/resolve/route.ts`
- `web/app/api/oracle/snapshot/route.ts`
- `web/hooks/usePlaceBet.ts`
- `web/hooks/usePosition.ts`
- `web/hooks/useClaim.ts`
- `web/hooks/useCreatorConfirm.ts`
- `web/components/BeliefSubmitForm.tsx`
- `web/tests/api-stats-overview.test.ts`
- `web/tests/use-place-bet.test.ts`
- `web/tests/api-positions.test.ts`
- `web/tests/api-creator-confirm.test.ts`
- `nodes/omen/CHANGELOG.md`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menghapus seluruh operator fallback `||` dan `??` serta alias multi-key pada parameter destructuring di seluruh rute `web/app/api`.
  2. Menghapus hardcoded dummy statistics (`148.5`, `1420000`, dll.) pada `web/app/api/stats/overview/route.ts` dan menegakkan database error propagation (HTTP 500).
  3. Menyelaraskan seluruh frontend hooks (`usePlaceBet`, `usePosition`, `useClaim`, `useCreatorConfirm`) dan form `BeliefSubmitForm` untuk mengirimkan payload kanonikal yang ketat.
  4. Memperbarui test suites (`api-stats-overview.test.ts`, `use-place-bet.test.ts`, `api-positions.test.ts`, `api-creator-confirm.test.ts`) untuk memvalidasi kontrak ketat.
  5. Menjalankan pengujian Vitest menyeluruh: 74/74 test files lulus, 383/383 tests passed.
  6. Menegakkan Zero-Comment Policy secara menyeluruh.
- **Ringkasan File Terpengaruh:**
  - Seluruh file di Target Lingkup File.
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Standarisasi parameter input/output API menghilangkan seluruh celah silent bug akibat data formatting mismatch.
