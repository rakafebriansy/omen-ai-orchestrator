# Local Tickets Directory (`tickets/`) — Omen

Direktori ini berfungsi sebagai pusat komando atau sumber kebenaran (*source of truth*) lokal untuk manajemen tugas node **Omen**.

## Aturan Penamaan File Tiket
Setiap file tiket baru yang dibuat di dalam direktori ini **WAJIB** dikonstruksikan menggunakan pedoman nama berikut:
`TICKET-[NOMOR]-[JUDUL-SINGKAT-KEBAB-CASE].md`
**Contoh Valid:** `TICKET-01-web-typescript-tailwind-setup.md`, `TICKET-04-prediction-market-contract.md`

## Boilerplate (Templat) Pembuatan Tiket Baru

```markdown
---
id: TICKET-[NOMOR]
title: [Judul Singkat Tugas]
status: Todo # Siklus Transisi Valid: Todo -> In Progress -> Done
priority: High # Siklus Valid: Low, Medium, High
labels: [Frontend, Backend, SmartContract, Feature, Bug, dsb]
---

# Deskripsi
[Tuliskan latar belakang instruksi, masalah, atau fitur yang ingin dibangun secara mendetail. AI Agent akan menginterpretasikan dan mengeksekusi kemauan Anda berdasarkan teks di sini.]

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] [Kriteria 1]
- [ ] [Kriteria 2]
- [ ] [Kriteria 3]

## Target Lingkup File (Affected Files)
- `path/ke/file.ext`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
  2. ...
- **Ringkasan File Terpengaruh:**
  - `path/ke/file/...`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - ...
```
