---
id: TICKET-31
title: Pembuatan API Route Simpan Pasar Baru
status: Todo
priority: Medium
labels: [Backend, API, Admin]
---

# Deskripsi
Mengembangkan API endpoint POST /api/markets khusus admin untuk menyimpan metadata pasar baru ke basis data Supabase.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memvalidasi otorisasi header wallet admin.
- [ ] Menyimpan contract_market_id, title, description, deadline, dan category.
- [ ] Menolak jika contract_market_id sudah pernah terdaftar.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
