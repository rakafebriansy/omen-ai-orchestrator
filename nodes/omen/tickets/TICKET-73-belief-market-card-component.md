---
id: TICKET-73
title: Pembuatan Komponen BeliefMarketCard (WHO, WHAT, WHEN, CONSENSUS, MONEY)
status: Done
priority: High
labels: [Frontend, UI, Component]
---

# Deskripsi
`BeliefMarketCard.tsx` adalah kartu utama yang merepresentasikan sebuah pasar keyakinan pada antarmuka OMEN V1. Kartu ini mengkomunikasikan 5 dimensi informasi secara simultan:
1. **WHO**: Handle atau nama kreator/penulis opini, dilengkapi lencana `✓ CONFIRMED` (jika kreator telah menandatangani konfirmasi EIP-712) atau `AI DETECTED`.
2. **WHAT**: Teks pernyataan keyakinan (*belief statement*) yang ringkas dan jelas.
3. **WHEN**: Countdown waktu penutupan pasar (*closing deadline*).
4. **CONSENSUS**: Rasio opini publik berdasarkan jumlah partisipan unik (`X% AGREE / Y% DISAGREE`).
5. **MONEY**: Rasio alokasi kapital on-chain (`X% AGREE / Y% DISAGREE` atau perbandingan ETH pool).
6. **STATUS & CTA**: Status badge (`OPEN`, `CLOSED`, `RESOLVED`) dan tombol navigasi langsung ke halaman detail `/market/[id]`.

> 🎨 **UI Style Preservation Note:**
> Style kartu — meliputi latar belakang kartu gelap dengan border subtle, efek hover glow/elevasi, badge status berwarna hijau emerald dan merah rose, progress bar konsensus, font sizing, dan padding — **WAJIB DIPERTAHANKAN** sesuai design system OMEN yang sudah berjalan. Jangan mengganti estetika visual dengan styling polos.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan komponen `BeliefMarketCard.tsx` di `omen/web/components/BeliefMarketCard.tsx`.
- [x] Menampilkan identitas kreator/author beserta lencana status verifikasi (`CONFIRMED` / `AI DETECTED`).
- [x] Menampilkan teks pernyataan belief dan hitung mundur sisa waktu deadline.
- [x] Menyajikan indikator perbandingan ganda: Konsensus Opini (Partisipan) dan Konsensus Kapital (ETH Pool).
- [x] Menavigasikan pengguna ke rute `/market/[id]` saat kartu atau tombol CTA diklik.
- [x] Mempertahankan style UI, tema dark mode, dan transisi hover yang elegan.
- [x] Menyusun unit test pada `web/tests/belief-market-card.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/BeliefMarketCard.tsx`
- `omen/web/tests/belief-market-card.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/belief-market-card.test.tsx` untuk 5 dimensi informasi, status badge, navigasi link `/market/[id]`, dan callback `onSelect`.
  2. Mengimplementasikan komponen `omen/web/components/BeliefMarketCard.tsx` dengan preservasi tema OpenZeppelin dark mode, styling progress bar konsensus (People vs Money), badge verifikasi creator EIP-712 vs AI, dan countdown waktu.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/belief-market-card.test.tsx` -> 4/4 passing 100%) dan ESLint manual (`npx eslint components/BeliefMarketCard.tsx tests/belief-market-card.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh file kode terkait.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/BeliefMarketCard.tsx`
  - `omen/web/tests/belief-market-card.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengisolasi fungsi hitung `formatCountdown` di level modul untuk mematuhi aturan pure function render compiler React 19 (`react-hooks/purity`).
