---
id: TICKET-76
title: Pembuatan Komponen PositionPanel (AGREE / DISAGREE Inline Flow)
status: Done
priority: High
labels: [Frontend, UI, Component, Web3]
---

# Deskripsi
`PositionPanel.tsx` adalah komponen antarmuka yang menggantikan modal taruhan lama (`BettingModal.tsx`). Sesuai arsitektur V1, penempatan posisi dilakukan melalui panel interaktif inline pada halaman detail pasar dengan terminologi keyakinan **AGREE** dan **DISAGREE**.

Alur pengguna dalam komponen:
1. Pilihan Side: Tombol sakelar AGREE (aksen hijau emerald) vs DISAGREE (aksen merah rose).
2. Input Nominal ETH: Input jumlah taruhan dengan tombol preset (0.01, 0.05, 0.1, MAX).
3. Kalkulasi Preview Dinamis: Estimasi persentase kepemilikan pool dan perkiraan payout potensial jika posisi menang.
4. Transaksi Web3 & Konfirmasi: Alur transaksi mulus: Connect Wallet (jika belum) -> Sign Transaction via Wallet -> Loading State (menunggu receipt) -> Notifikasi Sukses -> Refresh data pool pasar.

> 🎨 **UI Style Preservation Note:**
> Desain tombol AGREE/DISAGREE dengan highlight gradien/neon, input form styled Tailwind, tombol preset nominal, visual feedback loading spinner, dan alert box transaksi **WAJIB DIPERTAHANKAN** sesuai design system yang sudah ada di OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `PositionPanel.tsx` di `omen/web/components/PositionPanel.tsx`.
- [x] Menyediakan pemilihan side AGREE dan DISAGREE dengan styling visual yang kontras dan jelas.
- [x] Menyediakan input nominal ETH dengan validasi batas minimum dan format desimal.
- [x] Mengkalkulasi estimasi payout potensial secara dinamis berdasarkan kondisi pool saat ini.
- [x] Terhubung dengan hook Web3 (`usePosition` atau `useWriteContract`) untuk eksekusi on-chain dan sinkronisasi ke backend API.
- [x] Mempertahankan style UI, warna emerald/rose, dan responsivitas komponen.
- [x] Menyusun unit test pada `web/tests/position-panel.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/PositionPanel.tsx`
- `omen/web/tests/position-panel.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/position-panel.test.tsx` untuk pengujian seleksi side AGREE/DISAGREE, input nominal ETH & tombol presets (0.01, 0.05, 0.10, MAX), kalkulasi payout potensial, validasi saldo & batas minimum, penanganan submit transaksi, dan state loading.
  2. Mengimplementasikan komponen inline `omen/web/components/PositionPanel.tsx` dengan preservasi styling OpenZeppelin dark mode, warna emerald/rose, feedback loading spinner, alert konfirmasi/error, dan estimasi pool share dinamis.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/position-panel.test.tsx` -> 6/6 passing 100%) dan ESLint (`npx eslint components/PositionPanel.tsx tests/position-panel.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/PositionPanel.tsx`
  - `omen/web/tests/position-panel.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan struktur inline stateful panel untuk menggantikan modal dialog usang agar interaksi pasang posisi pada detail market berlangsung mulus tanpa context-switch.
