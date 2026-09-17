---
id: TICKET-85
title: Pembuatan API Route Submit Belief & Trigger On-Chain Market (POST /api/beliefs/submit)
status: Done
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
- [x] Mengimplementasikan `omen/web/app/api/beliefs/submit/route.ts` untuk `POST /api/beliefs/submit`.
- [x] Melakukan validasi payload terkonfirmasi via skema (statement, subject, timeframe, resolution rules, author, source).
- [x] Melakukan transaksi database terintegrasi ke tabel `beliefs` dan `belief_sources`.
- [x] Melakukan interaksi Web3 server-side via Viem untuk mengeksekusi `OmenFactory.createMarket` dan membaca alamat kontrak pasar yang dihasilkan.
- [x] Menyimpan record pasar ke tabel `markets` dengan contract address on-chain.
- [x] Menyusun unit test pada `omen/web/tests/api-beliefs-submit.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/submit/route.ts`
- `omen/web/lib/market/factory-client.ts`
- `omen/web/tests/api-beliefs-submit.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/api-beliefs-submit.test.ts` untuk pengujian kalkulasi keccak256 hash, validasi input required (`statement`, `raw_text`), pembuatan record `beliefs`, `belief_sources`, `markets`, `market_events`, dan eksekusi deployment via factory client.
  2. Mengembangkan modul `omen/web/lib/market/factory-client.ts` dengan fungsi `computeBeliefHashes` dan `createOnChainMarket` yang berinteraksi dengan smart contract `OmenFactory.createMarket` via Viem.
  3. Mengembangkan route handler `POST /api/beliefs/submit` pada `omen/web/app/api/beliefs/submit/route.ts` yang mengkoordinasikan penyimpanan metadata belief, pembuatan smart contract on-chain, dan inisialisasi pasar berstatus `OPEN`.
  4. Menjalankan pengujian vitest (317 tests pass di 55 test files), typecheck `tsc`, dan linter ESLint (0 error).
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/market/factory-client.ts`
  - `omen/web/app/api/beliefs/submit/route.ts`
  - `omen/web/tests/api-beliefs-submit.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan hashing deterministik `keccak256` untuk `beliefHash`, `sourceHash`, dan `resolutionHash` yang disimpan di blockchain untuk menjamin transparansi serta integritas data antara off-chain DB dan on-chain contract state.
