---
id: TICKET-06
title: Pembuatan Dialog Network Switcher Phantom EVM
status: Done
priority: Medium
labels: [Frontend, UI, Web3]
---

# Deskripsi
Membangun komponen dialog peringatan dan tombol perpindahan jaringan di `omen/web/components/NetworkSwitcherModal.tsx`. Komponen ini akan mendeteksi apakah dompet pengguna berada di jaringan yang benar (Arbitrum Sepolia, Chain ID 421614) dan menampilkan dialog pop-up persuasif jika dompet berada pada rantai yang tidak didukung.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`NetworkSwitcherModal.tsx`)
1. **Pemicu Dialog:**
   - Otomatis muncul saat dompet terhubung pada chain ID yang tidak cocok dengan Arbitrum Sepolia (421614).
2. **Backdrop dan Kontainer Modal:**
   - Backdrop: `fixed inset-0 bg-accent-navy/40 backdrop-blur-sm z-50 flex items-center justify-center p-4`.
   - Kotak Modal: `bg-white border border-border-subtle rounded-2xl max-w-md w-full p-6 shadow-xl text-center`.
3. **Elemen Visual:**
   - Ikon Peringatan: Lingkaran kuning/amber `w-12 h-12 bg-warning-soft text-warning-amber rounded-full flex items-center justify-center mx-auto mb-4`.
   - Judul: `text-xl font-bold text-accent-navy mb-2` bertuliskan "Wrong Network Detected".
   - Deskripsi: `text-sm text-text-muted mb-6` bertuliskan "Omen operates exclusively on Arbitrum Sepolia Testnet. Please switch your wallet network to continue."
   - Tombol Aksi: "Switch to Arbitrum Sepolia" (`w-full bg-primary-blue text-white hover:bg-primary-blue-hover py-3 rounded-lg font-semibold transition-all`).
4. **Indikator Status Network di Navbar:**
   - Badge kecil di navbar `bg-no-red-soft text-no-red text-xs font-mono font-medium px-2 py-1 rounded-md border border-no-red/20 flex items-center gap-1.5` saat wrong network.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Modal muncul secara visual saat status wrong network aktif.
- [x] Tombol switch network menampilkan state loading saat interaksi berlangsung.
- [x] Tersedia indikator visual status jaringan di samping tombol dompet.
- [x] Unit test komponen NetworkSwitcherModal lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/NetworkSwitcherModal.tsx`
- `omen/web/components/Navbar.tsx`
- `omen/web/tests/network-switcher.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Membuat komponen `NetworkSwitcherModal.tsx` berfitur tema ganda (Dark/Light Mode), ikon peringatan amber berkilau, kartu komparasi status jaringan aktif vs target (Arbitrum Sepolia Chain ID 421614), dan animasi state loading pada tombol switch.
  2. Memasang atribut aksesibilitas WAI-ARIA modal dialog (`role="dialog"`, `aria-modal="true"`, `aria-labelledby`, `aria-describedby`).
  3. Mengintegrasikan badge indikator status jaringan "Wrong Network" berdenyut (*animate-ping*) pada `Navbar.tsx` yang memicu terbukanya dialog switcher ketika diklik.
  4. Menyusun test suite `tests/network-switcher.test.tsx` dengan 5 unit tests yang menguji visibilitas modal, perbandingan jaringan, interaksi tombol switch, fungsi dismiss/close, serta integrasi badge di navbar (37/37 tests pass 100%).
  5. Menjalankan type checking `npx tsc --noEmit` (0 error) dan verifikasi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/NetworkSwitcherModal.tsx` [Created]
  - `omen/web/components/Navbar.tsx` [Modified]
  - `omen/web/tests/network-switcher.test.tsx` [Created]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Callback `onSwitchNetwork` dirancang asynchronous sehingga langsung kompatibel dengan method `switchChain` dari Wagmi/Viem saat integrasi Web3 dilakukan.
