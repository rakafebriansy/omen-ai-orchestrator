---
id: TICKET-80
title: Pembuatan Halaman Direktori & Ranking Kreator (/creators)
status: Done
priority: Medium
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Direktori Kreator (`app/creators/page.tsx`) menyajikan peringkat publik seluruh kreator/pembuat opini di platform OMEN. Direktori ini memungkinkan pengguna menemukan kreator dengan rekam jejak paling akurat atau keyakinan yang paling banyak memicu pergerakan pasar.

Fitur direktori:
1. **Opsi Pengurutan / Ranking**:
   - Most Confirmed Beliefs
   - Highest Accuracy (Win Rate)
   - Most Volume Generated (ETH)
   - Most Beliefs Created
2. **Kartu Kreator (`CreatorCard.tsx`)**: Menampilkan avatar, handle/address, statistik inti (akurasi %, jumlah belief, volume ETH), dan tombol navigasi ke profil lengkap.
3. **Pencarian**: Filter pencarian cepat berdasarkan nama/handle kreator atau alamat EVM.

> 🎨 **UI Style Preservation Note:**
> Desain kartu profil kreator, podium ranking (jika ada), tombol sorting pills, form search input, dan layout grid kartu **WAJIB DIPERTAHANKAN** sesuai design system yang berlaku di OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan halaman `app/creators/page.tsx` dan komponen `CreatorCard.tsx`.
- [x] Mengambil daftar kreator terurut dari endpoint `GET /api/creators` dengan opsi sorting dinamis.
- [x] Menyediakan filter pengurutan: `Highest Accuracy`, `Most Confirmed`, `Most Volume`, `Most Beliefs`.
- [x] Menyediakan input filter pencarian berbasis handle atau wallet address.
- [x] Merender kartu `CreatorCard` dalam grid responsif dengan navigasi ke `/creator/[address]`.
- [x] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [x] Menyusun unit test pada `web/tests/creators-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/creators/page.tsx`
- `omen/web/components/CreatorCard.tsx`
- `omen/web/tests/creators-page.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/creators-page.test.tsx` untuk pengujian ranking kreator, sorting pills (`Highest Accuracy`, `Most Confirmed`, `Most Volume`, `Most Beliefs`), pencarian berbasis teks/address, dan navigasi profil `/creator/[address]`.
  2. Mengimplementasikan komponen `omen/web/components/CreatorCard.tsx` dan halaman `omen/web/app/creators/page.tsx` dengan preservasi styling OpenZeppelin dark mode, lencana EIP-712 terverifikasi, grid metrik (akurasi, volume ETH, fee earned), dan transisi hover.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/creators-page.test.tsx` -> 4/4 passing 100%) dan ESLint (`npx eslint app/creators/page.tsx components/CreatorCard.tsx tests/creators-page.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/creators/page.tsx`
  - `omen/web/components/CreatorCard.tsx`
  - `omen/web/tests/creators-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menyertakan ranking badge dan sorting komputasi multi-kriteria untuk merangsang transparansi rekam jejak kreator opini terverifikasi EIP-712.
