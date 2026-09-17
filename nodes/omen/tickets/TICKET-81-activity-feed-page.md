---
id: TICKET-81
title: Pembuatan Halaman Feed Aktivitas Publik On-Chain (/activity)
status: Done
priority: Medium
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Feed Aktivitas (`app/activity/page.tsx`) menyajikan aliran aktivitas ekonomi dan sosial on-chain secara transparan dan mendekati waktu nyata (*real-time polling* setiap 30 detik). Halaman ini memberikan bukti nyata bahwa protokol OMEN aktif beroperasi.

Jenis aktivitas yang ditampilkan:
1. `AGREED with [Belief] for [Amount] ETH`
2. `DISAGREED with [Belief] for [Amount] ETH`
3. `CONFIRMED belief [Belief] via EIP-712 signature`
4. `CLAIMED payout of [Amount] ETH on [Belief]`
5. `RESOLVED market [Belief] -> [Outcome]`

Setiap item aktivitas memuat alamat dompet (terpotong `0x1234...5678`), tautan ke pasar terkait, tautan transaksi block explorer, nominal ETH, dan waktu relatif (misal: "2 mins ago").

> 🎨 **UI Style Preservation Note:**
> Tata letak daftar timeline, badge aksi bergradien (hijau untuk agree, merah untuk disagree, ungu/emas untuk confirm/claim), pulse live indicator, dan format waktu relatif **WAJIB DIPERTAHANKAN** sesuai design system yang berlaku di OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan halaman `app/activity/page.tsx` dan komponen `ActivityFeed.tsx`.
- [x] Mengambil daftar aktivitas dari endpoint `GET /api/activity` dengan pagination cursor-based atau limit.
- [x] Mengimplementasikan interval polling berkala (misal: 30 detik) untuk memuat transaksi terbaru.
- [x] Menampilkan tautan ke rute pasar `/market/[id]` dan explorer on-chain untuk setiap transaksi hash.
- [x] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [x] Menyusun unit test pada `web/tests/activity-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/activity/page.tsx`
- `omen/web/components/ActivityFeed.tsx`
- `omen/web/tests/activity-page.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test komprehensif `omen/web/tests/activity-page.test.tsx` untuk pengujian feed timeline aktivitas publik, filter tabs kategori (`All`, `Market Stakes`, `Confirmations`, `Payouts & Settled`), tautan navigasi pasar `/market/[id]`, dan tautan multi-chain block explorer (Sepolia & Robinhood).
  2. Mengimplementasikan komponen `omen/web/components/ActivityFeed.tsx` dan halaman `omen/web/app/activity/page.tsx` dengan polling background 30 detik, badge aksi dinamis (AGREE, DISAGREE, EIP-712, CLAIM, RESOLVE), dan kalkulasi waktu relatif.
  3. Memvalidasi dengan Vitest (`npx vitest run tests/activity-page.test.tsx` -> 3/3 passing 100%) dan ESLint (`npx eslint app/activity/page.tsx components/ActivityFeed.tsx tests/activity-page.test.tsx` -> 0 errors / 0 warnings).
  4. Menerapkan 100% Zero-Comment Policy pada seluruh berkas kode.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/activity/page.tsx`
  - `omen/web/components/ActivityFeed.tsx`
  - `omen/web/tests/activity-page.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengonfigurasi modul `getExplorerUrl` cerdas yang secara otomatis memetakan chain ID transaksi (Sepolia Etherscan vs Robinhood Testnet Explorer) untuk pengalaman navigasi on-chain multi-jaringan yang seamless.
