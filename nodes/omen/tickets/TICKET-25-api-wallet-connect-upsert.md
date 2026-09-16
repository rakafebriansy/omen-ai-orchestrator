---
id: TICKET-25
title: Pembuatan API Route Pendaftaran Wallet
status: Done
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan Route Handler `POST /api/wallet/connect` di `omen/web/app/api/wallet/connect/route.ts` untuk mendaftarkan akun pengguna baru saat dompet pertama kali terhubung.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Endpoint API
- **Metode:** `POST`
- **Request Body:** `{ wallet_address: string }`
- **Validasi:** Regex alamat EVM `^0x[a-fA-F0-9]{40}$`.
- **Logika:** Melakukan upsert record pada tabel `users`.
- **Response Sukses (200):** `{ success: true, user: { wallet_address, total_points, streak_count } }`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memvalidasi format alamat EVM dan menolak alamat yang tidak valid dengan status 400.
- [x] Berhasil melakukan upsert record di tabel users.
- [x] Unit test API route connect wallet lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/wallet/connect/route.ts`
- `omen/web/tests/api-wallet-connect.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan serverless Next.js API route handler `POST /api/wallet/connect` di `omen/web/app/api/wallet/connect/route.ts`.
  2. Menerapkan validasi ketat regex alamat EVM `^0x[a-fA-F0-9]{40}$`, penolakan format non-EVM dengan status 400, serta normalisasi alamat ke huruf kecil (`toLowerCase()`).
  3. Menggunakan `getSupabaseAdminClient()` untuk mengeksekusi operasi upsert pada tabel `users` dengan resolusi konflik pada `wallet_address`.
  4. Menyelaraskan kompatibilitas tipe generic `Database` di `omen/web/types/database.ts` dengan menggunakan type aliases agar kompatibel penuh dengan index signature `GenericSchema` PostgREST v2.
  5. Menulis unit test komprehensif di `omen/web/tests/api-wallet-connect.test.ts` (5 skenario uji: validasi payload, regex invalid EVM, upsert sukses, database error handling, dan kepatuhan Zero-Comment Policy).
  6. Memvalidasi seluruh test suite Vitest `npm run test` (25 file, 148 test lolos 100%) dan type check `npx tsc --noEmit` lolos tanpa error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/wallet/connect/route.ts` (Created)
  - `omen/web/types/database.ts` (Updated)
  - `omen/web/tests/api-wallet-connect.test.ts` (Created)
  - `nodes/omen/tickets/TICKET-25-api-wallet-connect-upsert.md` (Updated)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Alamat dompet EVM dinormalisasi (`toLowerCase()`) sebelum disimpan ke database Supabase guna menjamin konsistensi kueri case-insensitive lintas klien Web3 (seperti Wagmi, Viem, dan MetaMask/Phantom).
