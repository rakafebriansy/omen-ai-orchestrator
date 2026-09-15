---
id: TICKET-02
title: Setup Testing Suite Vitest
status: Done
priority: High
labels: [Frontend, Testing]
---

# Deskripsi
Mengonfigurasi test runner Vitest dan Testing Library React untuk pengujian unit komponen di omen/web.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Vitest dan @testing-library/react terpasang.
- [x] File konfigurasi vitest.config.ts siap digunakan.
- [x] Perintah npm run test berhasil menjalankan sample test.

## Target Lingkup File (Affected Files)
- `omen/web/vitest.config.mts`
- `omen/web/package.json`
- `omen/web/tests/setup.ts`
- `omen/web/tests/sample.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memasang dependensi pengujian `vitest`, `@testing-library/react`, `@testing-library/jest-dom`, `jsdom`, dan `@vitejs/plugin-react`.
  2. Menambahkan script perintah pengujian `"test": "vitest run"`, `"test:watch": "vitest"`, dan `"test:coverage": "vitest run --coverage"` pada `package.json`.
  3. Membuat berkas konfigurasi `vitest.config.mts` dengan plugin React, environment jsdom, setupFiles `./tests/setup.ts`, dan path alias `@/*`.
  4. Membuat file setup `./tests/setup.ts` yang mengimpor matcher `@testing-library/jest-dom/vitest`.
  5. Membuat sampel unit test `tests/sample.test.tsx` untuk menguji render komponen `HomePage`.
  6. Memvalidasi seluruh test suite berhasil lulus 100% via `npm run test`, `npm run lint`, dan `npx tsc --noEmit`.
- **Ringkasan File Terpengaruh:**
  - `omen/web/package.json`
  - `omen/web/package-lock.json`
  - `omen/web/vitest.config.mts`
  - `omen/web/tests/setup.ts`
  - `omen/web/tests/sample.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan ekstensi `.mts` untuk konfigurasi Vitest dengan `import.meta.dirname` guna menjamin kompatibilitas penuh ESM tanpa peringatan CommonJS loader.

