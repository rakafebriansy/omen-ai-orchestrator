---
id: TICKET-89
title: Pembuatan API Route Profil & Direktori Kreator (GET /api/creators & GET /api/creators/[address])
status: Todo
priority: Medium
labels: [Backend, API, Creators, Supabase]
---

# Deskripsi
Tiket ini menyediakan antarmuka API publik untuk menyajikan data direktori ranking kreator serta profil reputasi individual.

Endpoint yang dibangun:
1. `GET /api/creators`:
   - Mengambil daftar kreator dari tabel `creator_profiles`.
   - Mendukung parameter query: `sort` (`accuracy`, `confirmed_beliefs`, `volume_eth`, `total_beliefs`), `search` (handle / address), `limit`, `offset`.
   - Mengembalikan daftar profil kreator beserta agregasi akurasi dan ranking.
2. `GET /api/creators/[address]`:
   - Mengambil profil lengkap satu kreator berdasarkan alamat wallet EVM atau handle.
   - Melakukan agregasi relasi ke seluruh belief yang pernah dibuat/dikonfirmasi (status `Active`, `Resolved`), rincian akurasi persentase, dan total perputaran volume ETH.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan `omen/web/app/api/creators/route.ts` untuk `GET /api/creators`.
- [ ] Mengimplementasikan `omen/web/app/api/creators/[address]/route.ts` untuk `GET /api/creators/[address]`.
- [ ] Menyediakan kalkulasi persentase akurasi: `(correct_beliefs / resolved_beliefs) * 100` dengan perlindungan terhadap pembagian nol.
- [ ] Mengembalikan HTTP 404 jika alamat kreator tidak ditemukan dan HTTP 500 untuk error database.
- [ ] Menyusun unit test pada `omen/web/tests/api-creators.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/creators/route.ts`
- `omen/web/app/api/creators/[address]/route.ts`
- `omen/web/tests/api-creators.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
