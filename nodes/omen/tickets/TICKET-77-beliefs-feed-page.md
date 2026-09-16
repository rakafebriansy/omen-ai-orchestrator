---
id: TICKET-77
title: Pembuatan Halaman Katalog Beliefs (/beliefs)
status: Todo
priority: Medium
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Katalog Beliefs (`app/beliefs/page.tsx`) menyajikan indeks seluruh keyakinan sosial yang terdeteksi oleh AI maupun yang disubmit secara manual oleh komunitas. Halaman ini mencakup keyakinan yang masih berstatus `DETECTED` (belum diluncurkan sebagai pasar on-chain), `CONFIRMED`, maupun yang telah memiliki pasar aktif.

Fitur halaman:
- Filter Status: `All`, `AI Detected`, `Confirmed`, `Market Live`, `Resolved`.
- Search & Sorting: Berdasarkan kreator, kata kunci pernyataan, atau tingkat confidence AI.
- Render Grid/List: Menggunakan komponen `BeliefCard.tsx`.
- Tombol CTA: Tombol submit belief baru (`/create`) dan tautan ke pasar terkait jika sudah dibuka.

> 🎨 **UI Style Preservation Note:**
> Desain filter pills, container card grid, empty state visual, header typography, dan animasi transisi halaman **WAJIB DIPERTAHANKAN** sesuai tema OpenZeppelin dark mode OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan halaman `app/beliefs/page.tsx`.
- [ ] Mengambil daftar belief dari endpoint `GET /api/beliefs` dengan parameter filter status dan pagination.
- [ ] Menyediakan filter status tab: `All`, `AI Detected`, `Confirmed`, `Market Live`.
- [ ] Merender daftar belief menggunakan komponen `BeliefCard`.
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/beliefs-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/beliefs/page.tsx`
- `omen/web/tests/beliefs-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
