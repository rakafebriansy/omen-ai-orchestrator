---
id: TICKET-105
title: Fix Market Creation API Auth Header and Eliminate Hardcoded Keys
status: Done
priority: High
labels: [Frontend, Backend, Bug, Security, Web3, Markets]
---

# Deskripsi
Sinkronisasi database saat pembuatan pasar baru (`useAdminCreateMarket.ts`) mengalami kegagalan (401 Unauthorized) karena permintaan `POST /api/markets` tidak menyertakan header autentikasi (`x-admin-wallet`). Rute API memvalidasi otorisasi admin melalui `isAuthorizedAdmin()` yang memeriksa header `x-admin-wallet` terhadap daftar whitelist. Tiket ini menambahkan injeksi header autentikasi secara otomatis berdasarkan alamat wallet admin yang terhubung dan membersihkan nilai hardcoded kunci rahasia/wallet dummy dari implementasi rute API.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `useAdminCreateMarket.ts` menyertakan header `x-admin-wallet` yang sesuai saat memanggil `POST /api/markets`.
- [x] Jika wallet terhubung, nilai `address.toLowerCase()` dikirimkan; jika di mode mock, fallback ke `process.env.NEXT_PUBLIC_ADMIN_WALLET_ADDRESS`.
- [x] Kunci rahasia dummy `"omen-admin-2026"` dihapus dari array `validAdminKeys` di `web/app/api/markets/route.ts`.
- [x] Wallet dummy `"0xadmin99999999999999999999999999999999999"` dihapus dari array `validAdminWallets` di `web/app/api/markets/route.ts`.
- [x] Seluruh unit test suite pembuatan pasar tetap lulus tanpa regresi.

## Target Lingkup File (Affected Files)
- `web/hooks/useAdminCreateMarket.ts`
- `web/app/api/markets/route.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memodifikasi `useAdminCreateMarket.ts` pada blok fetch `POST /api/markets` untuk menginjeksi header `x-admin-wallet`.
  2. Memurnikan fungsi `isAuthorizedAdmin()` pada `web/app/api/markets/route.ts` dengan menghapus string fallback hardcoded.
  3. Memastikan variabel konfigurasi lingkungan di `web/tests/setup.ts` mendukung eksekusi pengujian otomatis.
- **Ringkasan File Terpengaruh:**
  - `web/hooks/useAdminCreateMarket.ts`
  - `web/app/api/markets/route.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Autentikasi berbasis wallet address dan API key kini 100% bersumber dari environment variables terkonfigurasi.
