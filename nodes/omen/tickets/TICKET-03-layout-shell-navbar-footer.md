---
id: TICKET-03
title: Pembuatan Layout Shell Navbar dan Footer
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun layout shell global aplikasi berestetika OpenZeppelin Institutional Web3 di `omen/web`, yang mencakup:
1. **Header / Navbar sticky** dengan efek *backdrop blur*, logo brand Omen, badge status testnet, link navigasi aktif dan hover, slot tombol dompet, serta menu hamburger drawer untuk perangkat mobile.
2. **Footer terstruktur** memuat ringkasan protokol, navigasi tautan cepat, link dokumentasi dan komunitas, serta indikator status jaringan testnet.
3. **Main content wrapper** yang menjamin footer tetap menempel di dasar layar (*sticky footer layout*) dengan pembatas lebar maksimal `max-w-7xl`.

## Spesifikasi Desain Antarmuka (UI Specification)

### 1. Komponen Navbar (`Navbar.tsx`)
- **Struktur Kontainer:** `sticky top-0 z-50 w-full bg-white/80 backdrop-blur-md border-b border-border-subtle h-16`.
- **Branding (Sisi Kiri):**
  - Teks Logo "OMEN" dengan tipografi `font-extrabold text-xl tracking-tight text-accent-navy`.
  - Pill badge "TESTNET" di samping logo: `bg-primary-blue-soft text-primary-blue text-xs font-mono font-semibold px-2.5 py-0.5 rounded-full border border-primary-blue/20`.
- **Navigasi Desktop (Sisi Tengah):**
  - Tautan menu: **Predictions** (`/predictions`), **Quests** (`/quests`), **Leaderboard** (`/leaderboard`), **My Bets** (`/my-bets`).
  - *State Inaktif:* `text-sm font-medium text-text-muted hover:text-accent-navy hover:bg-bg-subtle px-3 py-2 rounded-lg transition-colors`.
  - *State Aktif:* `text-sm font-semibold text-primary-blue bg-primary-blue-soft px-3 py-2 rounded-lg`.
- **Sisi Kanan:**
  - Area slot untuk tombol Connect Wallet dan indikator jaringan.
  - Tombol hamburger icon untuk tampilan mobile (`md:hidden`) dengan `aria-label="Toggle navigation menu"`.
- **Mobile Menu Drawer:**
  - Panel drawer responsif yang muncul saat hamburger diklik, menampilkan seluruh tautan navigasi vertikal dengan touch-target minimal `h-11`.

### 2. Komponen Footer (`Footer.tsx`)
- **Struktur Kontainer:** `w-full bg-bg-subtle border-t border-border-subtle py-10 mt-auto`.
- **Tata Letak Grid (4 Kolom pada Desktop, 1 Kolom pada Mobile):**
  - **Kolom 1 (Brand):** Logo Omen, deskripsi ringkas protokol, dan badge indikator status jaringan hijau bulat (`bg-yes-green animate-pulse`) bertuliskan "Arbitrum Sepolia Testnet".
  - **Kolom 2 (Platform):** Predictions Feed, Quests Farming, Points Leaderboard, My Bets.
  - **Kolom 3 (Developers):** Smart Contracts, GitHub Repo, Security Audit, Documentation.
  - **Kolom 4 (Community):** Komunitas X (Twitter), Discord, Telegram.
- **Baris Bawah (Bottom Sub-bar):** Copyright tahun berjalan, disclaimer *"Demonstration and testnet platform only"*, garis pemisah tipis `border-t border-border-subtle pt-6`.

### 3. Layout Root (`layout.tsx`)
- Wrapper `min-h-screen flex flex-col bg-bg-main text-text-primary antialiased`.
- Menyematkan `<Navbar />` di bagian atas, `<main className="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">{children}</main>`, dan `<Footer />` di bagian bawah.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Navbar sticky di posisi atas dengan efek blur dan border pembatas crisp 1px.
- [ ] Tautan navigasi aktif berubah warna dan background sesuai rute halaman yang sedang dibuka.
- [ ] Menu mobile hamburger dapat dibuka dan ditutup dengan mulus pada ukuran layar `< 768px`.
- [ ] Footer merender seluruh link kategori dan indikator status testnet secara rapi.
- [ ] Seluruh tombol dan link interaktif memenuhi standar kontras WCAG 2.1 AA dan memiliki atribut aksesibilitas ARIA labels.
- [ ] Unit test komponen Navbar dan Footer berhasil lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/layout.tsx`
- `omen/web/components/Navbar.tsx`
- `omen/web/components/Footer.tsx`
- `omen/web/tests/navbar.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
