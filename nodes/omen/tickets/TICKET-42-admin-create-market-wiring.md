---
id: TICKET-42
title: Integrasi Transaksi Admin Pembuatan Pasar
status: Todo
priority: Medium
labels: [Frontend, Web3, Admin]
---

# Deskripsi
Menghubungkan formulir admin pembuatan pasar ke fungsi createMarket on-chain dan menyimpan metadata judul ke Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Admin menandatangani transaksi createMarket di dompet.
- [ ] Mengambil marketId yang dihasilkan dari event transaksi on-chain.
- [ ] Menyimpan metadata pasar ke database melalui POST /api/markets.

## Target Lingkup File (Affected Files)
- `omen/web/components/AdminMarketCreateForm.tsx`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
