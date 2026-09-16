---
id: TICKET-05
title: Pembuatan Komponen Tombol Connect Wallet
status: Done
priority: High
labels: [Frontend, UI, Web3]
---

# Deskripsi
Membangun komponen antarmuka tombol `ConnectWalletButton` di `omen/web/components/ConnectWalletButton.tsx` untuk ditempatkan pada header navigasi. Komponen ini menangani representasi visual status koneksi dompet Phantom EVM, tampilan alamat dompet terpotong, saldo Native ETH, serta menu dropdown interaktif untuk menyalin alamat dan memutuskan koneksi dompet.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`ConnectWalletButton.tsx`)
1. **State Belum Terhubung (Disconnected):**
   - Tampilan tombol: `bg-primary-blue text-white hover:bg-primary-blue-hover px-4 py-2 rounded-lg font-semibold text-sm shadow-sm transition-all flex items-center gap-2`.
   - Ikon dompet SVG di sisi kiri teks "Connect Wallet".
2. **State Sedang Menghubungkan (Connecting / Loading):**
   - Tombol disabled dengan spinner animasi berputar dan teks "Connecting...".
3. **State Berhasil Terhubung (Connected):**
   - Kontainer terpadu: `flex items-center bg-bg-subtle border border-border-subtle rounded-lg p-1 hover:border-slate-300 transition-all`.
   - Saldo ETH: `px-3 text-xs font-mono font-medium text-text-muted hidden sm:inline-block` (contoh: "0.45 ETH").
   - Chip Alamat: `flex items-center gap-2 bg-white px-3 py-1.5 rounded-md border border-border-subtle shadow-xs text-xs font-mono font-semibold text-accent-navy`.
   - Indikator Status: Titik hijau bulat `w-2 h-2 rounded-full bg-yes-green`.
   - Alamat terpotong: `0x12...34`.
4. **Dropdown Menu Interaktif:**
   - Muncul saat chip alamat diklik (`absolute right-0 mt-2 w-48 bg-white border border-border-subtle rounded-xl shadow-lg py-1 z-50`).
   - Opsi 1: "Copy Address" (dengan feedback teks sementara "Copied!").
   - Opsi 2: "View on Explorer" (link eksternal ke Arbiscan Sepolia).
   - Opsi 3: "Disconnect" dengan teks merah `text-no-red hover:bg-no-red-soft`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Tombol merender teks 'Connect Wallet' saat belum terhubung.
- [x] Menampilkan format alamat terpotong (0x12...34) dan saldo saat terhubung.
- [x] Dropdown menu interaktif dapat dibuka dan ditutup dengan opsi Copy Address dan Disconnect.
- [x] Dilengkapi atribut aksesibilitas ARIA labels (`aria-haspopup`, `aria-expanded`).
- [x] Unit test komponen ConnectWalletButton lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/ConnectWalletButton.tsx`
- `omen/web/components/Navbar.tsx`
- `omen/web/tests/wallet-button.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat komponen `ConnectWalletButton.tsx` dengan dukungan 3 status koneksi (`disconnected`, `connecting`, `connected`), alamat terpotong EVM, saldo ETH, dan dropdown menu interaktif.
  2. Mengimplementasikan fitur interaktif dropdown: tombol "Copy Address" dengan indikator feedback "Copied!" selama 2 detik via `navigator.clipboard`, tautan "View on Explorer" ke Arbiscan Sepolia, opsi "Disconnect", serta outside-click listener untuk menutup dropdown.
  3. Memasang atribut aksesibilitas WAI-ARIA lengkap (`aria-haspopup="menu"`, `aria-expanded`, `aria-label`, `role="menu"`, `role="menuitem"`).
  4. Mengintegrasikan `ConnectWalletButton` ke dalam `Navbar.tsx` (menggantikan tombol statis pada tampilan desktop maupun drawer navigasi mobile).
  5. Membuat test suite komprehensif `tests/wallet-button.test.tsx` mencakup 8 unit tests yang menguji seluruh transisi status, interaksi dropdown, clipboard copy, dan pemutusan koneksi.
  6. Memverifikasi seluruh pengujian (32/32 tests pass 100%), type check TypeScript lulus tanpa error (`npx tsc --noEmit`), serta kepatuhan mutlak terhadap Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/ConnectWalletButton.tsx` [Created]
  - `omen/web/components/Navbar.tsx` [Modified]
  - `omen/web/tests/wallet-button.test.tsx` [Created]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Komponen dirancang sebagai pure UI mock state component yang theme-aware (`useTheme`), siap untuk diintegrasikan dengan wagmi/viem provider pada tiket integrasi Web3 lanjutan tanpa memerlukan refactoring tata letak atau aksesibilitas.
