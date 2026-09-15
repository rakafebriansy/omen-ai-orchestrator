---
id: TICKET-01
title: Setup Next.js dan Tailwind OpenZeppelin Theme
status: Done
priority: High
labels: [Frontend, Tooling]
---

# Deskripsi
Mengonfigurasi Next.js dengan TypeScript dan Tailwind CSS v4 menggunakan token tema OpenZeppelin Institutional Web3 di direktori omen/web secara CSS-first (@theme).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Project Next.js berjalan dengan TypeScript strict mode aktif.
- [x] Tailwind CSS v4 terkonfigurasi dengan palet warna OpenZeppelin di globals.css (@theme).
- [x] Halaman awal dapat dirender tanpa error kompilasi.

## Target Lingkup File (Affected Files)
- `omen/web/package.json`
- `omen/web/postcss.config.mjs`
- `omen/web/app/globals.css`
- `omen/web/tsconfig.json`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memasang dependensi TypeScript (`typescript`, `@types/node`, `@types/react`, `@types/react-dom`), Tailwind CSS v4 (`tailwindcss`, `@tailwindcss/postcss`), dan helper kelas (`clsx`, `tailwind-merge`).
  2. Mengonfigurasi `tsconfig.json` dengan `strict: true` dan alias `@/*`, serta menghapus `jsconfig.json`.
  3. Mengonfigurasi `postcss.config.mjs` untuk mengaktifkan plugin `@tailwindcss/postcss`.
  4. Mengonfigurasi token tema OpenZeppelin di `omen/web/app/globals.css` menggunakan sintaks CSS-first Tailwind v4 `@theme` (tanpa komentar kode sesuai ZERO-COMMENT POLICY).
  5. Mengonversi `layout.js` dan `page.js` menjadi `layout.tsx` dan `page.tsx`, serta menghapus `page.module.css`.
  6. Memvalidasi kompilasi melalui `npx tsc --noEmit`, `npm run lint`, dan `npm run build`.
- **Ringkasan File Terpengaruh:**
  - `omen/web/package.json`
  - `omen/web/tsconfig.json`
  - `omen/web/postcss.config.mjs`
  - `omen/web/app/globals.css`
  - `omen/web/app/layout.tsx`
  - `omen/web/app/page.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengadopsi arsitektur Tailwind CSS v4 CSS-first (`@theme`) di dalam `globals.css` sehingga tidak membutuhkan `tailwind.config.ts` dan tidak memerlukan `autoprefixer` terpisah.

