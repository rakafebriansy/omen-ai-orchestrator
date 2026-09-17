---
id: TICKET-77
title: Pembuatan Halaman Katalog Beliefs (/beliefs)
status: Done
priority: Medium
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Katalog Beliefs (`app/beliefs/page.tsx`) menyajikan indeks seluruh keyakinan sosial yang terdeteksi oleh AI maupun yang disubmit secara manual oleh komunitas. Halaman ini mencakup keyakinan yang masih berstatus `DETECTED` (belum diluncurkan sebagai pasar on-chain), `CONFIRMED`, maupun yang telah memiliki pasar aktif.

Fitur halaman:
- Filter Status: `All`, `AI Detected`, `Confirmed`, `Market Live`, `Resolved`.
- Search & Sorting: Berdasarkan kreator, kata kunci pernyataan, atau tingkat confidence AI.
- Render Grid/List: Menggunakan komponen `BeliefCard.tsx`.
- Tombol CTA: Tombol submit belief baru (`/create`) dan tautan ke pasar terkait jika sudah dibuka.

> 🎨 **UI Style Preservation Note:**
> Desain filter pills, container card grid, empty state visual, header typography, dan animasi transisi halaman **WAJIB DIPERTAHANKAN** sesuai tema OpenZeppelin dark mode OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan halaman `app/beliefs/page.tsx`.
- [x] Mengambil daftar belief dari endpoint `GET /api/beliefs` dengan parameter filter status dan pagination.
- [x] Menyediakan filter status tab: `All`, `AI Detected`, `Confirmed`, `Market Live`.
- [x] Merender daftar belief menggunakan komponen `BeliefCard`.
- [x] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [x] Menyusun unit test pada `web/tests/beliefs-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/beliefs/page.tsx`
- `omen/web/tests/beliefs-page.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/beliefs-page.test.tsx` untuk pengujian judul halaman, navigasi CTA submit `/create`, filter tab status (`All`, `AI Detected`, `Confirmed`, `Market Live`), dan pencarian teks bebas (kata kunci pernyataan / kreator).
  2. Mengimplementasikan halaman katalog `omen/web/app/beliefs/page.tsx` dengan integrasi dinamis data `/api/beliefs`, komponen `BeliefCard`, filter status chips, input pencarian responsif, dan state empty/loading.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/beliefs-page.test.tsx` -> 3/3 passing 100%) dan ESLint (`npx eslint app/beliefs/page.tsx tests/beliefs-page.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/beliefs/page.tsx`
  - `omen/web/tests/beliefs-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengimplementasikan client-side filtering and search fallback yang tangguh untuk memastikan antarmuka tetap responsif bahkan saat data remote sedang dimuat atau mengalami jeda jaringan.
