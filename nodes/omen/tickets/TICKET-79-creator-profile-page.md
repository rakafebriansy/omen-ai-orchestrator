---
id: TICKET-79
title: Pembuatan Halaman Profil Kreator (/creator/[address])
status: Todo
priority: Medium
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Profil Kreator (`app/creator/[address]/page.tsx`) menyajikan rekam jejak reputasi dan akurasi prediksi seorang pembuat opini/kreator. Halaman ini menggantikan model leaderboard poin gamifikasi lama dengan model reputasi sosial berbasis rekam jejak keyakinan nyata.

Informasi yang disajikan:
1. **Header Kreator**: Handle, ENS/Address, Avatar, Bio, dan status verifikasi wallet.
2. **Kartu Statistik Reputasi**:
   - Total Beliefs Tracked
   - Confirmation Rate (% belief yang dikonfirmasi resmi via EIP-712)
   - Win Rate / Accuracy (% prediksi yang terbukti benar setelah resolusi)
   - Total Volume Generated (total ETH yang dipertaruhkan publik pada keyakinan kreator ini)
3. **Tabs Rekam Jejak**:
   - `Active Beliefs`: Keyakinan yang pasarnya masih berjalan.
   - `Resolved Beliefs`: Keyakinan yang sudah selesai beserta hasil akhirnya (BENAR / SALAH).
   - `All Origins`: Daftar sumber postingan/tweet asli yang pernah diindeks.

> 🎨 **UI Style Preservation Note:**
> Tata letak header profil, kartu metrik reputasi, tab navigasi rekam jejak, badge persentase akurasi, dan perenderan daftar kartu **WAJIB DIPERTAHANKAN** sesuai standar estetika antarmuka OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan halaman `app/creator/[address]/page.tsx`.
- [ ] Mengambil data profil dan agregasi statistik dari `GET /api/creators/[address]`.
- [ ] Menampilkan kartu metrik: Total Beliefs, Confirmation Rate, Accuracy Rate, dan Total Volume Generated.
- [ ] Menyediakan tab navigasi untuk melihat `Active Beliefs` dan `Resolved Beliefs`.
- [ ] Menghubungkan setiap belief ke halaman detail pasarnya.
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/creator-profile-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/creator/[address]/page.tsx`
- `omen/web/components/CreatorProfileHeader.tsx`
- `omen/web/tests/creator-profile-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
