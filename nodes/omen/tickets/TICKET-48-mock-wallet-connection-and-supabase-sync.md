---
id: TICKET-48
title: Integrasi Mock Wallet Connection & Auto-Registration ke Supabase
status: Done
priority: High
labels: [Frontend, Web3, Auth, Supabase, Integration]
---

# Deskripsi
Mengintegrasikan komponen `ConnectWalletButton.tsx` dan shell navigasi `Navbar.tsx` dengan mock wallet provider saat `NEXT_PUBLIC_USE_MOCK_CONTRACT="true"`. Saat pengguna mengklik tombol "Connect Wallet", simulator menghubungkan alamat demo (`0x71C...B29`) secara instan dan otomatis memanggil `POST /api/wallet/connect` ke Supabase untuk mendaftarkan akun pengguna ke tabel `users`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `ConnectWalletButton.tsx` mendeteksi mode mock dan menghubungkan demo wallet tanpa memicu modal ekstensi browser.
- [x] Setelah terkoneksi, memicu pemanggilan `POST /api/wallet/connect` dengan payload `{ wallet_address }` untuk upsert ke basis data Supabase.
- [x] Menampilkan saldo virtual ETH pengguna dan badge "Demo Wallet (Mock Mode)" pada antarmuka.
- [x] Tombol disconnect mereset status koneksi dan mengembalikan UI ke keadaan semula.
- [x] Menyediakan unit test suite Vitest di `omen/web/tests/mock-wallet-connect.test.tsx` dengan kelulusan 100%.

## Target Lingkup File (Affected Files)
- [ConnectWalletButton.tsx:L1](../../../../omen/web/components/ConnectWalletButton.tsx#L1)
- [mock-wallet-connect.test.tsx:L1](../../../../omen/web/tests/mock-wallet-connect.test.tsx#L1)
- [wallet-button.test.tsx:L1](../../../../omen/web/tests/wallet-button.test.tsx#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengintegrasikan `mockPredictionMarket.getDemoWallet()` ke dalam `ConnectWalletButton.tsx`.
  2. Menambahkan pemicu asynchronous `fetch("/api/wallet/connect")` untuk auto-registrasi/upsert dompet pengguna ke basis data Supabase saat status terhubung.
  3. Menambahkan lencana "Demo Wallet (Mock Mode)" pada dropdown menu wallet.
  4. Menyusun unit test suite Vitest di `web/tests/mock-wallet-connect.test.tsx` dan memvalidasi kelulusan 100% (10/10 tests pass).
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/ConnectWalletButton.tsx`, `omen/web/tests/mock-wallet-connect.test.tsx`, `omen/web/tests/wallet-button.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan isolasi mock wallet yang kompatibel dengan contract adapter simulator dan zero runtime comment.
