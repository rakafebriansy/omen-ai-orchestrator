---
id: TICKET-24
title: Pembuatan Supabase Database Client Helper
status: Todo
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
- [ ] Client Supabase tervalidasi mengekspor helper instance yang aman.
- [ ] Tipe data TypeScript mencakup seluruh skema tabel secara strict.
- [ ] Unit test helper Supabase lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/lib/supabase.ts`
- `omen/web/types/database.ts`
- `omen/web/tests/supabase.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
