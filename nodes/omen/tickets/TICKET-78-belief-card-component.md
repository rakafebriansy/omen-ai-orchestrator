---
id: TICKET-78
title: Pembuatan Komponen BeliefCard (Compact Belief & Status Badge)
status: Done
priority: Medium
labels: [Frontend, UI, Component]
---

# Deskripsi
`BeliefCard.tsx` adalah komponen kartu representasi belief yang lebih kompak dibandingkan `BeliefMarketCard`. Komponen ini berfokus pada konten pernyataan opini, profil author, tautan sumber asli, skor keyakinan AI (*confidence score*), serta status verifikasi kreator.

Elemen-elemen kartu:
1. Handle/Nama Kreator & Avatar identicon/avatar URL.
2. Teks Pernyataan Keyakinan (*statement*).
3. Badge Status: `AI DETECTED`, `CONFIRMED`, atau `MARKET OPEN`.
4. Metadata ekstraksi: Subjek, Aset pembanding, Arah prediksi, Target waktu.
5. Tautan Sumber Asli (ikon eksternal ke Twitter/Warpcast).
6. Aksi: Tautan "View Market" (jika pasar sudah dibuat) atau "Create Market" (jika belum).

> 🎨 **UI Style Preservation Note:**
> Style kartu — border halus dengan warna netral gelap, badge pill berwarna tegas, font sizing teks pernyataan, dan efek hover glow — **WAJIB DIPERTAHANKAN** sesuai design system yang berlaku di OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan komponen `BeliefCard.tsx` di `omen/web/components/BeliefCard.tsx`.
- [x] Menampilkan author handle, statement, dan link ke sumber asli.
- [x] Merender badge status verifikasi (`AI DETECTED` / `CONFIRMED`) dan confidence badge.
- [x] Menyediakan tombol navigasi kondisional ke detail pasar jika market_id tersedia.
- [x] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [x] Menyusun unit test pada `web/tests/belief-card.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/BeliefCard.tsx`
- `omen/web/tests/belief-card.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/belief-card.test.tsx` untuk pengujian rendering profil author, pernyataan keyakinan, badge verifikasi & confidence AI, tautan sumber eksternal, dan aksi kondisional View/Create Market.
  2. Mengimplementasikan komponen `omen/web/components/BeliefCard.tsx` dengan preservasi styling OpenZeppelin dark mode, metadata chips, dan transisi hover.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/belief-card.test.tsx` -> 5/5 passing 100%) dan ESLint (`npx eslint components/BeliefCard.tsx tests/belief-card.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/BeliefCard.tsx`
  - `omen/web/tests/belief-card.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menyediakan fallback aksi dinamis: jika `marketId` telah terbit, tautan langsung mengarah ke `/market/[id]`, jika belum, tombol memanggil handler atau navigasi pembuatan pasar `/create`.
