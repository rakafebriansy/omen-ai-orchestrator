---
id: TICKET-05
title: Pembuatan Komponen Tombol Connect Wallet
status: Todo
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
- [ ] Tombol merender teks 'Connect Wallet' saat belum terhubung.
- [ ] Menampilkan format alamat terpotong (0x12...34) dan saldo saat terhubung.
- [ ] Dropdown menu interaktif dapat dibuka dan ditutup dengan opsi Copy Address dan Disconnect.
- [ ] Dilengkapi atribut aksesibilitas ARIA labels (`aria-haspopup`, `aria-expanded`).
- [ ] Unit test komponen ConnectWalletButton lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/ConnectWalletButton.tsx`
- `omen/web/tests/wallet-button.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
