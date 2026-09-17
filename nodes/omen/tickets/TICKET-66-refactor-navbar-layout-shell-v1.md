---
id: TICKET-66
title: Refactor Navbar, Footer & Layout Shell Navigasi V1
status: Done
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
- [x] Memperbarui daftar tautan navigasi pada `Navbar.tsx` menjadi: `Markets` (`/markets`), `Beliefs` (`/beliefs`), `Creators` (`/creators`), dan `Activity` (`/activity`).
- [x] Menambahkan tombol CTA "Submit Belief" dengan routing ke `/create` pada header di samping `ConnectWalletButton`.
- [x] Memperbarui tautan footer pada `Footer.tsx` untuk merefleksikan arsitektur V1 dan link explorer multi-chain.
- [x] Mempertahankan seluruh styling CSS/Tailwind, animasi navbar sticky, burger menu mobile, dan logo OMEN resmi.
- [x] Menyusun/memperbarui unit test pada `web/tests/navbar.test.tsx` dan `web/tests/footer.test.tsx` agar lulus 100% dengan Zero-Comment Policy.

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
  1. Memperbarui test suite `web/tests/navbar.test.tsx` dan `web/tests/footer.test.tsx` untuk memvalidasi navigasi V1 (`/markets`, `/beliefs`, `/creators`, `/activity`, `/create`) dan tautan dual explorer.
  2. Merefaktor `web/components/Navbar.tsx` dengan daftar navigasi baru dan tombol CTA "Submit Belief" beraksen royal cobalt (`bg-primary-blue`).
  3. Merefaktor `web/components/Footer.tsx` dengan deskripsi OMEN V1 Social Belief Protocol, badge Dual-Testnet, tautan multi-explorer (Sepolia & Robinhood), dan link halaman V1.
  4. Memvalidasi 100% kelulusan unit test dan static linting tanpa error dan mematuhi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/Navbar.tsx`
  - `omen/web/components/Footer.tsx`
  - `omen/web/tests/navbar.test.tsx`
  - `omen/web/tests/footer.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Tombol "Submit Belief" ditempatkan di header desktop dan menu mobile untuk akses instan ke 3-step wizard creation flow (`/create`).
  - Menjaga konsistensi tema OpenZeppelin dark mode dan aksen border emerald seam pada sticky header.
