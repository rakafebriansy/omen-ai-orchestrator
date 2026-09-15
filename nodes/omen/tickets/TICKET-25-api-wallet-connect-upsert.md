---
id: TICKET-25
title: Pembuatan API Route Pendaftaran Wallet
status: Todo
priority: High
labels: [Backend, API]
---

# Deskripsi
Mengembangkan API endpoint POST /api/wallet/connect untuk melakukan upsert record user baru saat dompet pertama kali terhubung.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menerima parameter wallet_address dan memvalidasi format alamat EVM.
- [ ] Menyimpan record baru jika belum ada, atau memperbarui last_seen jika sudah ada.
- [ ] Mengembalikan profil user dan total poin terkini.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/wallet/connect/route.ts`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
