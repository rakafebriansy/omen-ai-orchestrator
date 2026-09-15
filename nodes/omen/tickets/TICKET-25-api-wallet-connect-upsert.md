---
id: TICKET-25
title: Pembuatan API Route Pendaftaran Wallet
status: Todo
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
- [ ] Memvalidasi format alamat EVM dan menolak alamat yang tidak valid dengan status 400.
- [ ] Berhasil melakukan upsert record di tabel users.
- [ ] Unit test API route connect wallet lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/wallet/connect/route.ts`
- `omen/web/tests/api-wallet-connect.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
