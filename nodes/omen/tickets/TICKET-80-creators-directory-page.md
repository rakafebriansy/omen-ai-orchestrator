---
id: TICKET-80
title: Pembuatan Halaman Direktori & Ranking Kreator (/creators)
status: Todo
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
- [ ] Mengimplementasikan halaman `app/creators/page.tsx` dan komponen `CreatorCard.tsx`.
- [ ] Mengambil daftar kreator terurut dari endpoint `GET /api/creators` dengan opsi sorting dinamis.
- [ ] Menyediakan filter pengurutan: `Highest Accuracy`, `Most Confirmed`, `Most Volume`, `Most Beliefs`.
- [ ] Menyediakan input filter pencarian berbasis handle atau wallet address.
- [ ] Merender kartu `CreatorCard` dalam grid responsif dengan navigasi ke `/creator/[address]`.
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/creators-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/creators/page.tsx`
- `omen/web/components/CreatorCard.tsx`
- `omen/web/tests/creators-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
