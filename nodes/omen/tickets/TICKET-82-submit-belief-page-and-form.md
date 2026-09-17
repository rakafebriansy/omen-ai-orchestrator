---
id: TICKET-82
title: Pembuatan Halaman & Formulir Submit Belief 3-Langkah (/create)
status: Done
priority: High
labels: [Frontend, UI, Form, AI]
---

# Deskripsi
Halaman Pembuatan & Pengajuan Keyakinan (`app/create/page.tsx`) memungkinkan pengguna mengonversi teks opini sosial mentah (hasil copy-paste dari Twitter/Warpcast/post lain) menjadi pasar keyakinan terstruktur on-chain melalui panduan alur 3 langkah (*3-Step Wizard*):

1. **Langkah 1: Input Teks Mentah**:
   - Teks opini mentah (*raw post text*).
   - Tautan sumber asli (*source URL*).
   - Handle/nama pembuat opini (*author handle*).
2. **Langkah 2: Ekstraksi AI & Validasi**:
   - Panggilan ke `POST /api/beliefs/extract`.
   - Menampilkan hasil parsing JSON AI: Subjek, Aset Pembanding, Arah Prediksi, Jangka Waktu (*Timeframe*), Oracle Feed Rekomendasi, dan Skor Keyakinan (*Confidence Score*).
   - Pengguna dapat mengoreksi atau mengedit field jika ada kekeliruan ekstraksi.
3. **Langkah 3: Konfirmasi & Peluncuran Pasar On-Chain**:
   - Pengguna mengonfirmasi data final.
   - Panggilan ke `POST /api/beliefs/submit` yang memicu pencatatan database dan pembuatan kontrak pasar `OmenMarket` via `OmenFactory`.
   - Mengalihkan pengguna langsung ke halaman pasar baru `/market/[id]`.

> 🎨 **UI Style Preservation Note:**
> Desain wizard multi-langkah (progress stepper, form inputs dengan focus ring ungu/emerald, kartu pratinjau JSON terstruktur, tombol submit dengan visual loading state, dan error alerts) **WAJIB DIPERTAHANKAN** sesuai design system yang berlaku di OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan halaman `app/create/page.tsx` dan komponen `BeliefSubmitForm.tsx`.
- [x] Menyediakan form langkah 1 untuk memasukkan teks mentah, URL sumber, dan handle author dengan validasi input.
- [x] Menghubungkan proses analisis AI ke `POST /api/beliefs/extract` dan merender editor pratinjau di langkah 2.
- [x] Menghubungkan tombol peluncuran di langkah 3 ke `POST /api/beliefs/submit` dan menangani loading on-chain.
- [x] Mengarahkan pengguna ke `/market/[id]` setelah pasar berhasil dibuat.
- [x] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [x] Menyusun unit test pada `web/tests/create-belief-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/create/page.tsx`
- `omen/web/components/BeliefSubmitForm.tsx`
- `omen/web/tests/create-belief-page.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/create-belief-page.test.tsx` untuk 3 langkah alur wizard (Step 1 input teks mentah -> Step 2 review ekstraksi parameter AI -> Step 3 konfirmasi & deploy on-chain -> auto redirect `/market/[id]`).
  2. Mengimplementasikan komponen `omen/web/components/BeliefSubmitForm.tsx` dan halaman `omen/web/app/create/page.tsx` dengan progress stepper visual, indikator skor confidence AI, kartu review ringkasan parameter pasar, dan loading status deploy.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/create-belief-page.test.tsx` -> 3/3 passing 100%) dan ESLint (`npx eslint app/create/page.tsx components/BeliefSubmitForm.tsx tests/create-belief-page.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/create/page.tsx`
  - `omen/web/components/BeliefSubmitForm.tsx`
  - `omen/web/tests/create-belief-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengintegrasikan pembungkusan `Suspense` pada `CreateBeliefPage` untuk memastikan kompatibilitas client hook `useSearchParams` saat parsing parameter teks/author dari URL.
