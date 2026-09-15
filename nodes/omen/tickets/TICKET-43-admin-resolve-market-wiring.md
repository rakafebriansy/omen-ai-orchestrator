---
id: TICKET-43
title: Integrasi Transaksi Admin Resolusi Pasar
status: Todo
priority: Medium
labels: [Frontend, Web3, Admin]
---

# Deskripsi
Menghubungkan antarmuka `AdminMarketResolutionTable` ke fungsi `resolveMarket` smart contract on-chain dan memperbarui status pasar di Supabase via `POST /api/markets/[id]/resolve`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Alur Integrasi Admin Resolve
1. Admin memilih hasil Yes atau No dan menandatangani transaksi `resolveMarket(marketId, result)`.
2. Setelah transaksi on-chain sukses, memanggil API `POST /api/markets/[id]/resolve` untuk memperbarui status pasar di database.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Status pasar di smart contract terkunci permanen pada hasil pemenang.
- [ ] Status pasar di database Supabase terbarui ke resolved_yes atau resolved_no.
- [ ] Tabel resolusi admin memperbarui daftar pasar yang tersisa.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useAdminResolveMarket.ts`
- `omen/web/components/AdminMarketResolutionTable.tsx`
- `omen/web/tests/admin-resolve-market.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
