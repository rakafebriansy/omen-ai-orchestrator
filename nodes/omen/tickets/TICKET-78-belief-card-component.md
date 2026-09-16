---
id: TICKET-78
title: Pembuatan Komponen BeliefCard (Compact Belief & Status Badge)
status: Todo
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
- [ ] Mengimplementasikan komponen `BeliefCard.tsx` di `omen/web/components/BeliefCard.tsx`.
- [ ] Menampilkan author handle, statement, dan link ke sumber asli.
- [ ] Merender badge status verifikasi (`AI DETECTED` / `CONFIRMED`) dan confidence badge.
- [ ] Menyediakan tombol navigasi kondisional ke detail pasar jika market_id tersedia.
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/belief-card.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/BeliefCard.tsx`
- `omen/web/tests/belief-card.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
