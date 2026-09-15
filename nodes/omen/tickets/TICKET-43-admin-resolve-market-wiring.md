---
id: TICKET-43
title: Integrasi Transaksi Admin Resolusi Pasar
status: Todo
priority: Medium
labels: [Frontend, Web3, Admin]
---

# Deskripsi
Menghubungkan antarmuka admin resolusi ke fungsi resolveMarket on-chain dan memperbarui status pasar di database Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Admin mengeksekusi transaksi on-chain resolveMarket(marketId, result).
- [ ] Status pasar di smart contract terkunci permanen.
- [ ] Memperbarui status di database melalui POST /api/markets/[id]/resolve.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketResolutionTable.tsx`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
