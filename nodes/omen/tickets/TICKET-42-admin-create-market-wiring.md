---
id: TICKET-42
title: Integrasi Transaksi Admin Pembuatan Pasar
status: Todo
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
- [ ] Pasar baru berhasil terdaftar di smart contract blockchain.
- [ ] Metadata pasar tersimpan secara sinkron di tabel markets Supabase.
- [ ] Formulir mereset input dan menampilkan notifikasi sukses.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useAdminCreateMarket.ts`
- `omen/web/components/AdminMarketCreateForm.tsx`
- `omen/web/tests/admin-create-market.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
