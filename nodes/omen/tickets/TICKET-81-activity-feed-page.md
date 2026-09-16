---
id: TICKET-81
title: Pembuatan Halaman Feed Aktivitas Publik On-Chain (/activity)
status: Todo
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
- [ ] Mengimplementasikan halaman `app/activity/page.tsx` dan komponen `ActivityFeed.tsx`.
- [ ] Mengambil daftar aktivitas dari endpoint `GET /api/activity` dengan pagination cursor-based atau limit.
- [ ] Mengimplementasikan interval polling berkala (misal: 30 detik) untuk memuat transaksi terbaru.
- [ ] Menampilkan tautan ke rute pasar `/market/[id]` dan explorer on-chain untuk setiap transaksi hash.
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/activity-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/activity/page.tsx`
- `omen/web/components/ActivityFeed.tsx`
- `omen/web/tests/activity-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
