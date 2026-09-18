---
id: TICKET-121
title: Update Omen Brand Logo and Integrate Category Tab Icons on Landing Page
status: Done
priority: High
labels: [Frontend, UI, Branding, LandingPage, Icons]
---

# Deskripsi
Memperbarui aset logo resmi platform Omen secara global menggunakan file `logo-omen 1.png` pada Navbar, Footer, Favicon Metadata, dan aset statis `images/logo.png`. Selain itu, mengintegrasikan logo/ikon visual dari direktori `public/icons/` (`hot.webp`, `eth.webp`, `btc.webp`, `arb.webp`, `macro.webp`) pada komponen tabbing *Trending Belief Markets* di Landing Page (`TrendingMarketsTeaser.tsx`) untuk meningkatkan impresi visual dan hierarki navigasi pasar prediksi.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Logo Omen diperbarui secara global menggunakan aset `/logo-omen 1.png` pada `Navbar.tsx`, `Footer.tsx`, `app/layout.tsx`, dan `public/images/logo.png`.
- [x] Komponen `TrendingMarketsTeaser.tsx` mengintegrasikan ikon grafis kategori dari `public/icons/` (`hot.webp`, `eth.webp`, `btc.webp`, `arb.webp`, `macro.webp`) pada tabbing `All`, `ETH`, `BTC`, `ARB`, dan `Macro`.
- [x] Filter kategori pada `TrendingMarketsTeaser.tsx` mencocokkan kategori dan keyword aset secara akurat.
- [x] Seluruh 77 test suites (401 unit tests) lulus 100% pada Vitest dan `npx tsc --noEmit` lolos 0 error.
- [x] Mematuhi secara mutlak Zero-Comment Policy pada seluruh file `.ts` dan `.tsx` yang dimodifikasi.

## Target Lingkup File (Affected Files)
- `omen/web/public/images/logo.png`
- `omen/web/components/Navbar.tsx`
- `omen/web/components/Footer.tsx`
- `omen/web/app/layout.tsx`
- `omen/web/components/landing/TrendingMarketsTeaser.tsx`
- `omen/web/tests/landing.test.tsx`

---

## AI Execution Log dan Output

- **Langkah Teknis Tereksekusi:**
  1. Menyalin dan menyelaraskan aset logo kanonikal dari `web/public/logo-omen 1.png` ke `web/public/images/logo.png`.
  2. Memperbarui referensi logo di `Navbar.tsx` dan `Footer.tsx` serta favicon metadata di `app/layout.tsx` ke `/logo-omen 1.png`.
  3. Memperbarui tabbing *Trending Belief Markets* pada `TrendingMarketsTeaser.tsx` dengan menambahkan list `CATEGORY_TABS` yang menyematkan ikon `hot.webp`, `eth.webp`, `btc.webp`, `arb.webp`, dan `macro.webp`.
  4. Mengimplementasikan fungsi filter cerdas untuk mencocokkan kategori spesifik (`eth`, `btc`, `arb`, `macro`) beserta keyword terkait pada statement pasar.
  5. Memperbarui assertions pada `tests/landing.test.tsx` dan memverifikasi kelulusan 100% pada 77 test suites (401 unit tests).
  6. Menjalankan `graphify update` untuk menyelaraskan AST Knowledge Graph node Omen.
- **Ringkasan File Terpengaruh:**
  - `omen/web/public/images/logo.png`
  - `omen/web/components/Navbar.tsx`
  - `omen/web/components/Footer.tsx`
  - `omen/web/app/layout.tsx`
  - `omen/web/components/landing/TrendingMarketsTeaser.tsx`
  - `omen/web/tests/landing.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Penyalinan aset ke `images/logo.png` sekaligus pembaruan referensi ke `/logo-omen 1.png` menjamin kompatibilitas ganda (*backward compatibility*) jika terdapat referensi legacy.
