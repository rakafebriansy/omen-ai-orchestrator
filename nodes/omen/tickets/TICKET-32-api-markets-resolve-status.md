---
id: TICKET-32
title: Pembuatan API Route Pembaruan Status Pasar
status: Todo
priority: Medium
labels: [Backend, API, Admin]
---

# Deskripsi
Mengembangkan API endpoint POST /api/markets/[id]/resolve khusus admin untuk memperbarui status pasar menjadi resolved_yes atau resolved_no.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memvalidasi otorisasi wallet admin.
- [ ] Mengubah status pasar di tabel markets dan mencatat resolution_source.
- [ ] Mencegah perubahan status jika pasar sudah pernah diresolve sebelumnya.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/[id]/resolve/route.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
