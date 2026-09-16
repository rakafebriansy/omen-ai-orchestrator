---
id: TICKET-66
title: Refactor Navbar, Footer & Layout Shell Navigasi V1
status: Todo
priority: High
labels: [Frontend, UI, Layout, Navigation]
---

# Deskripsi
Seiring transformasi OMEN ke V1 Social Belief Market, struktur navigasi global aplikasi perlu diselaraskan dengan mental model baru:
- **Tautan Navigasi Baru**: Markets (`/markets`), Beliefs (`/beliefs`), Creators (`/creators`), Activity (`/activity`).
- **Tautan Navigasi Lama**: Quests (`/quests`), Leaderboard (`/leaderboard`), dan My Bets (`/my-bets`) dinonaktifkan dari menu utama (diarsipkan untuk fase selanjutnya).
- **Aksi Header**: Tombol CTA utama "Submit Belief" (`/create` atau modal trigger) dan tombol `ConnectWalletButton` terintegrasi.
- **Footer**: Update tautan dokumen, GitHub repo, smart contract explorer link, dan status network indicator.

> 🎨 **UI Style Preservation Note:**
> Style visual Navbar, Footer, dan Layout Shell — termasuk tema OpenZeppelin dark mode, styling glassmorphism, warna borders, brand logo OMEN, efek hover, active link indicators, dan typography — **WAJIB DIPERTAHANKAN**. Penyesuaian hanya terbatas pada label tautan, href tujuan, dan penambahan tombol aksi CTA "Submit Belief" tanpa merusak estetika desain yang sudah matang.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memperbarui daftar tautan navigasi pada `Navbar.tsx` menjadi: `Markets` (`/markets`), `Beliefs` (`/beliefs`), `Creators` (`/creators`), dan `Activity` (`/activity`).
- [ ] Menambahkan tombol CTA "Submit Belief" dengan routing ke `/create` pada header di samping `ConnectWalletButton`.
- [ ] Memperbarui tautan footer pada `Footer.tsx` untuk merefleksikan arsitektur V1 dan link explorer multi-chain.
- [ ] Mempertahankan seluruh styling CSS/Tailwind, animasi navbar sticky, burger menu mobile, dan logo OMEN resmi.
- [ ] Menyusun/memperbarui unit test pada `web/tests/navbar.test.tsx` dan `web/tests/footer.test.tsx` agar lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/Navbar.tsx`
- `omen/web/components/Footer.tsx`
- `omen/web/app/layout.tsx`
- `omen/web/tests/navbar.test.tsx`
- `omen/web/tests/footer.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
