---
id: TICKET-62
title: Integrasi Live API Data pada Trending Markets Teaser dan Quests Teaser Landing Page
status: Done
priority: Medium
labels: [Frontend, Backend, Feature, Supabase, LandingPage]
---

# Deskripsi
Komponen beranda `components/landing/TrendingMarketsTeaser.tsx` dan `components/landing/QuestsTeaser.tsx` masih menggunakan data tiruan yang di-hardcode di dalam file. `TrendingMarketsTeaser.tsx` memiliki array `MARKETS` (baris 32–144), sedangkan `QuestsTeaser.tsx` memiliki array statis `DAYS` (baris 14–22) dan `ACTIVE_QUESTS` (baris 24–49).

Tiket ini bertujuan untuk menghubungkan kedua komponen beranda tersebut ke API Supabase backend (`GET /api/markets` dan `GET /api/quests`), sehingga pengguna baru langsung disajikan data pasar terpopuler dan quest aktif yang riil saat mengunjungi landing page.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Menghapus dataset statis `MARKETS` pada `omen/web/components/landing/TrendingMarketsTeaser.tsx` dan menggantinya dengan fetch dinamis dari `GET /api/markets?status=active`.
- [x] Menyediakan *skeleton loader* untuk kartu pasar tren di beranda saat data sedang dimuat.
- [x] Menghubungkan daftar quest aktif pada `omen/web/components/landing/QuestsTeaser.tsx` dengan endpoint `GET /api/quests`.
- [x] Menyediakan fallback tampilan visual yang rapi jika basis data belum memiliki pasar aktif atau quest.
- [x] Seluruh unit tests Vitest di `omen/web` lulus 100% dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/landing/TrendingMarketsTeaser.tsx`
- `omen/web/components/landing/QuestsTeaser.tsx`
- `omen/web/tests/landing.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan test suite TDD pada `web/tests/landing.test.tsx` untuk memverifikasi live API fetching pada teaser pasar tren dan teaser quest.
  2. Menghapus dataset statis `MARKETS` dari `web/components/landing/TrendingMarketsTeaser.tsx` dan menghubungkannya dengan `GET /api/markets`.
  3. Menghubungkan `web/components/landing/QuestsTeaser.tsx` dengan `GET /api/quests` untuk menampilkan 3 misi teratas aktif dan streak roadmap dinamis.
  4. Memvalidasi kelulusan seluruh 9/9 unit tests pada `tests/landing.test.tsx` dengan kepatuhan Zero-Comment Policy 100%.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/landing/TrendingMarketsTeaser.tsx`
  - `omen/web/components/landing/QuestsTeaser.tsx`
  - `omen/web/tests/landing.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Komponen teaser beranda mengintegrasikan loading skeleton state yang seragam dengan design system protokol.
