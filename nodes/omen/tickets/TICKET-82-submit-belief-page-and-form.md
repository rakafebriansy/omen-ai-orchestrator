---
id: TICKET-82
title: Pembuatan Halaman & Formulir Submit Belief 3-Langkah (/create)
status: Todo
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
- [ ] Mengimplementasikan halaman `app/create/page.tsx` dan komponen `BeliefSubmitForm.tsx`.
- [ ] Menyediakan form langkah 1 untuk memasukkan teks mentah, URL sumber, dan handle author dengan validasi input Zod.
- [ ] Menghubungkan proses analisis AI ke `POST /api/beliefs/extract` dan merender editor pratinjau di langkah 2.
- [ ] Menghubungkan tombol peluncuran di langkah 3 ke `POST /api/beliefs/submit` dan menangani loading on-chain.
- [ ] Mengarahkan pengguna ke `/market/[id]` setelah pasar berhasil dibuat.
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/create-belief-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/create/page.tsx`
- `omen/web/components/BeliefSubmitForm.tsx`
- `omen/web/tests/create-belief-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
