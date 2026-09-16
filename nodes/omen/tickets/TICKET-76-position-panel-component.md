---
id: TICKET-76
title: Pembuatan Komponen PositionPanel (AGREE / DISAGREE Inline Flow)
status: Todo
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
- [ ] Mengimplementasikan `PositionPanel.tsx` di `omen/web/components/PositionPanel.tsx`.
- [ ] Menyediakan pemilihan side AGREE dan DISAGREE dengan styling visual yang kontras dan jelas.
- [ ] Menyediakan input nominal ETH dengan validasi batas minimum dan format desimal.
- [ ] Mengkalkulasi estimasi payout potensial secara dinamis berdasarkan kondisi pool saat ini.
- [ ] Terhubung dengan hook Web3 (`usePosition` atau `useWriteContract`) untuk eksekusi on-chain dan sinkronisasi ke backend API.
- [ ] Mempertahankan style UI, warna emerald/rose, dan responsivitas komponen.
- [ ] Menyusun unit test pada `web/tests/position-panel.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/PositionPanel.tsx`
- `omen/web/tests/position-panel.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
