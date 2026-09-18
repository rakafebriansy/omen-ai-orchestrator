---
id: TICKET-114
title: AI Provider API Key Cleanup and Migration to OpenRouter Environment Standards
status: Done
priority: High
labels: [Backend, AI, Environment, Refactor, Security]
---

# Deskripsi
Pembersihan menyeluruh terhadap penggunaan environment variable `process.env.AI_API_KEY` dari seluruh codebase Omen untuk menegakkan standardisasi integrasi OpenRouter API yang aman, eksplisit, dan kompatibel dengan live deployment di Vercel.

### Akar Masalah:
1. **Inkonsistensi Naming Environment Variable:**
   - Sebagian modul dan helper AI di `web/lib/ai/` merujuk ke variable legacy `AI_API_KEY`, sedangkan dokumentasi dan setup Vercel menggunakan `OPENROUTER_API_KEY`.
2. **Ketiadaan Pemisahan Jelas antara Mock Test vs Production AI:**
   - Helper ekstraksi Social Belief AI memerlukan inisialisasi yang strictly memprioritaskan `OPENROUTER_API_KEY` resmi dengan opsi mock offline `MOCK_AI_RESPONSE` saat berjalan di Vitest environment.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Hapus seluruh referensi `process.env.AI_API_KEY` dari seluruh codebase, modul AI, route handlers, dan test files.
- [x] Standardisasi inisialisasi AI client pada `web/lib/ai/openrouter.ts` hanya menggunakan `process.env.OPENROUTER_API_KEY`.
- [x] Pastikan test suite offline memanfaatkan `MOCK_AI_RESPONSE` atau mock handler tanpa memicu koneksi network eksternal liar.
- [x] 100% test suites lulus (77 files, 395 unit tests) dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `web/lib/ai/openrouter.ts`
- `web/lib/ai/mockOpenRouter.ts`
- `web/app/api/beliefs/extract/route.ts`
- `web/app/api/beliefs/submit/route.ts`
- `web/tests/`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Melakukan audit dan grep terhadap seluruh pemanggilan `AI_API_KEY` di repository.
  2. Menghapus referensi `AI_API_KEY` dan menyelaraskan ke `OPENROUTER_API_KEY` pada seluruh modul backend dan integrasi AI.
  3. Memvalidasi skenario AI extraction dengan unit test `tests/api-beliefs-extract.test.ts`.
  4. Memverifikasi kelulusan test suite dan kompilasi TypeScript `npx tsc --noEmit`.
- **Ringkasan File Terpengaruh:**
  - `web/lib/ai/openrouter.ts`
  - `web/lib/ai/mockOpenRouter.ts`
  - `web/app/api/beliefs/extract/route.ts`
  - `web/app/api/beliefs/submit/route.ts`
- **Catatan dan Keputusan Arsitektural:**
  - Mengisolasi client OpenRouter sebagai single source of truth untuk AI extraction, memastikan secret key tidak bocor ke client-side.
