---
id: TICKET-24
title: Pembuatan Supabase Database Client Helper
status: Done
priority: High
labels: [Backend, Database]
---

# Deskripsi
Menginisialisasi helper client Supabase di `omen/web/lib/supabase.ts` dan tipe TypeScript otomatis di `omen/web/types/database.ts` untuk serverless route handlers dan client components.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Helper dan Interface
- Inisialisasi Supabase Client membaca `process.env.NEXT_PUBLIC_SUPABASE_URL` dan `process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY`.
- Helper Server Client untuk route handlers membaca `SUPABASE_SERVICE_ROLE_KEY`.
- Tipe TypeScript `Database` mencakup interface tabel `User`, `Quest`, `PointsEvent`, `Market`, `Bet`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Client Supabase tervalidasi mengekspor helper instance yang aman.
- [x] Tipe data TypeScript mencakup seluruh skema tabel secara strict.
- [x] Unit test helper Supabase lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/lib/supabase.ts`
- `omen/web/types/database.ts`
- `omen/web/tests/api-supabase.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menginstal `@supabase/supabase-js` sebagai SDK resmi Supabase client.
  2. Menyusun definisi tipe TypeScript di `omen/web/types/database.ts` (`PointsSource`, `MarketStatus`, `BetSide`, entitas `User`, `Quest`, `PointsEvent`, `Market`, `Bet`, serta interface skema `Database` lengkap).
  3. Membangun modul helper di `omen/web/lib/supabase.ts` yang mengekspor fungsi `getSupabaseClient()` (browser/anon) dan `getSupabaseAdminClient()` (server role key untuk bypass RLS pada off-chain backend engine).
  4. Menulis unit test suite di `omen/web/tests/api-supabase.test.ts` menguji inisialisasi, singleton reuse, fallback error handling, pembersihan instance, dan Zero-Comment Policy.
  5. Memvalidasi eksekusi pengujian `npm run test` (24 test files, 143 tests pass 100%) serta type checking `npx tsc --noEmit` lolos tanpa galat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/package.json` & `package-lock.json` (Updated)
  - `omen/web/types/database.ts` (Created)
  - `omen/web/lib/supabase.ts` (Created)
  - `omen/web/tests/api-supabase.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-24-supabase-database-client-helper.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengadopsi pola cached singleton dengan utilitas reset (`resetSupabaseClients`) untuk memastikan efisiensi koneksi pada lingkungan serverless Next.js sekaligus menjaga isolasi state pada pengujian unit.
