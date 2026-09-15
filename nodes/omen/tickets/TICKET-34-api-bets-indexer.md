---
id: TICKET-34
title: Pembuatan API Route Indexer Taruhan
status: Todo
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan API endpoint POST /api/bets/index untuk mencatat event transaksi taruhan on-chain dan memberikan bonus poin partisipasi.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menerima tx_hash, market_id, wallet_address, side, dan amount.
- [ ] Mencegah duplikasi pencatatan tx_hash dengan constraint unik.
- [ ] Menambahkan poin aktivitas partisipasi taruhan ke points_events.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/bets/index/route.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
