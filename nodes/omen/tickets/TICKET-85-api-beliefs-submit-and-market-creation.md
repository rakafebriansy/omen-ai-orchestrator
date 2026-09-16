---
id: TICKET-85
title: Pembuatan API Route Submit Belief & Trigger On-Chain Market (POST /api/beliefs/submit)
status: Todo
priority: High
labels: [Backend, API, Web3, Factory]
---

# Deskripsi
Setelah pengguna meninjau dan mengonfirmasi hasil ekstraksi teks belief pada halaman `/create`, endpoint `POST /api/beliefs/submit` dipanggil untuk:
1. Menyimpan data entitas keyakinan ke tabel `beliefs` dengan status awal `DETECTED`.
2. Menyimpan metadata sumber postingan ke tabel `belief_sources`.
3. Menghitung deterministik hash: `beliefHash`, `sourceHash`, dan `resolutionHash` menggunakan `keccak256`.
4. Memicu pembuatan instans smart contract `OmenMarket` melalui pemanggilan server-side / viem client ke kontrak `OmenFactory.createMarket(...)` (menggunakan admin/deployer key yang aman).
5. Menerima address `OmenMarket` yang baru terbentuk dan menyimpannya ke tabel `markets` (status: `OPEN`).
6. Mengembalikan payload `{ belief_id, market_id, contract_address, tx_hash }`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan `omen/web/app/api/beliefs/submit/route.ts` untuk `POST /api/beliefs/submit`.
- [ ] Melakukan validasi payload terkonfirmasi via skema Zod (statement, subject, timeframe, resolution rules, author, source).
- [ ] Melakukan transaksi database terintegrasi ke tabel `beliefs` dan `belief_sources`.
- [ ] Melakukan interaksi Web3 server-side via Viem untuk mengeksekusi `OmenFactory.createMarket` dan membaca alamat kontrak pasar yang dihasilkan.
- [ ] Menyimpan record pasar ke tabel `markets` dengan contract address on-chain.
- [ ] Menyusun unit test pada `omen/web/tests/api-beliefs-submit.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/submit/route.ts`
- `omen/web/lib/market/factory-client.ts`
- `omen/web/tests/api-beliefs-submit.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
