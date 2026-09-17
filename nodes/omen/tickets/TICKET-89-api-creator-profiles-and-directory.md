---
id: TICKET-89
title: Pembuatan API Route Profil & Direktori Kreator (GET /api/creators & GET /api/creators/[address])
status: Done
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
- [x] Mengimplementasikan `omen/web/app/api/creators/route.ts` untuk `GET /api/creators`.
- [x] Mengimplementasikan `omen/web/app/api/creators/[address]/route.ts` untuk `GET /api/creators/[address]`.
- [x] Menyediakan kalkulasi persentase akurasi: `(correct_beliefs / resolved_beliefs) * 100` dengan perlindungan terhadap pembagian nol.
- [x] Mengembalikan HTTP 404 jika alamat kreator tidak ditemukan dan HTTP 500 untuk error database.
- [x] Menyusun unit test pada `omen/web/tests/api-creators.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/creators/route.ts`
- `omen/web/app/api/creators/[address]/route.ts`
- `omen/web/tests/api-creators.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/api-creators.test.ts` yang memverifikasi kepatuhan Zero-Comment, endpoint direktori kreator dengan pagination dan filter pencarian, endpoint detail profil kreator dengan kalkulasi akurasi, penanganan HTTP 404 saat not found, dan penanganan HTTP 500 untuk error query database.
  2. Mengembangkan route handler `GET /api/creators` pada `omen/web/app/api/creators/route.ts` dengan query dinamis untuk sorting, pagination, search text, dan kalkulasi field `accuracy_percentage`.
  3. Mengembangkan route handler `GET /api/creators/[address]` pada `omen/web/app/api/creators/[address]/route.ts` dengan pencarian via wallet address atau handle, serta agregasi data relasi beliefs.
  4. Menjalankan pengujian vitest, linter ESLint, dan typechecking tsc (100% pass, 0 lint error, 0 comment).
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/creators/route.ts`
  - `omen/web/app/api/creators/[address]/route.ts`
  - `omen/web/tests/api-creators.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Kalkulasi `accuracy_percentage` dilakukan dengan membagi `correct_count` terhadap `resolved_count` dengan penanganan pembagian nol (menghasilkan 0% jika belum ada belief yang selesai di-resolve), dan dibulatkan ke 2 digit desimal.
