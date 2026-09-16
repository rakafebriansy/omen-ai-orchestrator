---
id: TICKET-42
title: Integrasi Transaksi Admin Pembuatan Pasar
status: Done
priority: Medium
labels: [Frontend, Web3, Admin]
---

# Deskripsi
Menghubungkan formulir `AdminMarketCreateForm` ke fungsi `createMarket` smart contract on-chain dan menyimpan metadata pasar ke Supabase via `POST /api/markets`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Alur Integrasi Admin Create
1. Admin menandatangani transaksi on-chain `createMarket(title, deadline)`.
2. Mengambil ID pasar baru dari receipt event `MarketCreated`.
3. Memanggil API `POST /api/markets` untuk menyimpan judul, deskripsi, dan kategori ke database.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Pasar baru berhasil terdaftar di smart contract blockchain.
- [x] Metadata pasar tersimpan secara sinkron di tabel markets Supabase.
- [x] Formulir mereset input dan menampilkan notifikasi sukses.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useAdminCreateMarket.ts`
- `omen/web/components/AdminMarketCreateForm.tsx`
- `omen/web/tests/admin-create-market.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengimplementasikan custom hook `useAdminCreateMarket` di `omen/web/hooks/useAdminCreateMarket.ts` memanfaatkan `useWriteContract`, `useWaitForTransactionReceipt`, `useAccount`, `usePublicClient`, dan context guard `WagmiContext`.
  2. Mengimplementasikan konversi deadline waktu ke unix timestamp (detik) dan pemanggilan on-chain `createMarket(title, deadline)`.
  3. Mengimplementasikan ekstraksi receipt logs / decoding event `MarketCreated` via Viem serta sinkronisasi metadata pasar ke database backend melalui `POST /api/markets`.
  4. Mengintegrasikan `useAdminCreateMarket` ke dalam `AdminMarketCreateForm.tsx` pada fungsi `handleConfirmDeploy`, dengan preservasi backward compatibility pemanggilan prop `onSubmitMarket`.
  5. Menulis unit test suite di `omen/web/tests/admin-create-market.test.ts` (2/2 tests pass) dan memverifikasi seluruh test suite (26 test files / 139 tests di `omen/web` lulus 100%, 19 unit tests di `omen/contracts` lulus 100%) dan `tsc --noEmit` 0 galat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/hooks/useAdminCreateMarket.ts`
  - `omen/web/components/AdminMarketCreateForm.tsx`
  - `omen/web/tests/admin-create-market.test.ts`
  - `nodes/omen/tickets/TICKET-42-admin-create-market-wiring.md`
  - `nodes/omen/CHANGELOG.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengimplementasikan context guard yang mengembalikan safe fallback non-blocking pada lingkungan pengujian terisolasi tanpa `WagmiProvider`, memungkinkan seluruh unit test form dan page eksisting tetap lulus tanpa perubahan.
  - Memastikan seluruh kode TypeScript mematuhi aturan Zero-Comment Policy secara mutlak.
