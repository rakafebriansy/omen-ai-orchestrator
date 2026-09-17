---
id: TICKET-106
title: Fix Market Resolution API Auth Header and Eliminate Hardcoded Fallback Secrets
status: Done
priority: High
labels: [Frontend, Backend, Bug, Security, Web3, Resolution]
---

# Deskripsi
Sinkronisasi status resolusi pasar ke basis data (`useAdminResolveMarket.ts`) mengalami kegagalan (401 Unauthorized) karena permintaan `POST /api/markets/[id]/resolve` tidak menyertakan header otorisasi admin (`x-admin-wallet`). Rute API memvalidasi kredensial admin melalui fungsi `isAuthorizedAdmin()`. Tiket ini menambahkan injeksi header `x-admin-wallet` pada pemanggilan fetch resolusi dan menghapus nilai hardcoded master keys dan fallback wallets dari rute API resolusi.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `useAdminResolveMarket.ts` menyertakan header `x-admin-wallet` yang sesuai saat memanggil `POST /api/markets/${marketId}/resolve`.
- [x] Nilai wallet admin dikirim secara dinamis (menggunakan `address.toLowerCase()` atau fallback ke `process.env.NEXT_PUBLIC_ADMIN_WALLET_ADDRESS`).
- [x] Kunci rahasia dummy `"omen-admin-2026"` dihapus dari array `validAdminKeys` di `web/app/api/markets/[id]/resolve/route.ts`.
- [x] Wallet dummy `"0xadmin99999999999999999999999999999999999"` dihapus dari array `validAdminWallets` di `web/app/api/markets/[id]/resolve/route.ts`.
- [x] Seluruh unit test suite resolusi pasar berjalan normal tanpa regresi.

## Target Lingkup File (Affected Files)
- `web/hooks/useAdminResolveMarket.ts`
- `web/app/api/markets/[id]/resolve/route.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memodifikasi `useAdminResolveMarket.ts` untuk menyertakan header `x-admin-wallet` saat melakukan request fetch sinkronisasi resolusi pasar.
  2. Menghapus hardcoded string `"omen-admin-2026"` dan `"0xadmin99999999999999999999999999999999999"` pada `web/app/api/markets/[id]/resolve/route.ts`.
  3. Memastikan seluruh acceptance criteria terverifikasi lewat vitest automated test suites.
- **Ringkasan File Terpengaruh:**
  - `web/hooks/useAdminResolveMarket.ts`
  - `web/app/api/markets/[id]/resolve/route.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Autentikasi resolusi kini terlindungi dan tersinkronisasi antar hook frontend dan API backend.
