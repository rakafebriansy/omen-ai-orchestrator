---
id: TICKET-86
title: Refactor API Route Markets V1 (GET /api/markets & GET /api/markets/[id])
status: Todo
priority: High
labels: [Backend, API, Markets, Supabase]
---

# Deskripsi
Endpoint pasar yang sudah ada (`GET /api/markets`) perlu diselaraskan dengan skema V1 dan model Social Belief.

Perubahan yang dilakukan:
1. `GET /api/markets`:
   - Melakukan relasi (*join*) tabel `markets` dengan `beliefs`, `belief_sources`, dan `creator_profiles`.
   - Mengkalkulasi metrik dinamis:
     - `opinion_consensus`: persentase partisipan `agree_count / (agree_count + disagree_count)`.
     - `capital_consensus`: persentase dana `agree_pool / (agree_pool + disagree_pool)`.
   - Mendukung filter tab: `trending` (kombinasi volume & partisipan), `newest`, `ending_soon`, `most_volume`, `confirmed`.
   - Mendukung pencarian berbasis teks keyakinan atau author handle.
2. `GET /api/markets/[id]`:
   - Mengambil detail lengkap satu pasar berdasarkan UUID atau `contract_address`, mencakup snapshot oracle, riwayat event, dan status resolusi.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memperbarui `omen/web/app/api/markets/route.ts` untuk mendukung skema V1 dan filter tab discovery.
- [ ] Mengimplementasikan `omen/web/app/api/markets/[id]/route.ts` untuk detail lengkap pasar.
- [ ] Menghitung rasio konsensus opini dan rasio pool kapital secara akurat dan aman terhadap pembagian dengan nol.
- [ ] Mengembalikan relasi data belief dan profil kreator dalam bentuk JSON terstruktur.
- [ ] Menyusun unit test pada `omen/web/tests/api-markets-v1-get.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/markets/route.ts`
- `omen/web/app/api/markets/[id]/route.ts`
- `omen/web/tests/api-markets-v1-get.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
