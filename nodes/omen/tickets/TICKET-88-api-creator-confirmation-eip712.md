---
id: TICKET-88
title: Pembuatan API Route Konfirmasi Kreator EIP-712 (POST /api/beliefs/[id]/confirm)
status: Done
priority: High
labels: [Backend, API, EIP712, Creator]
---

# Deskripsi
Salah satu inovasi penting dalam OMEN V1 adalah **Creator Confirmation** tanpa biaya gas (gasless) menggunakan tanda tangan kriptografis EIP-712 off-chain. Fitur ini memungkinkan sang pembuat opini memvalidasi secara resmi bahwa keyakinan yang terdeteksi AI benar-benar mencerminkan pandangannya.

Alur teknis endpoint `POST /api/beliefs/[id]/confirm`:
1. Menerima payload: `{ signature: `0x...`, creator_address: `0x...`, chain_id: number, timestamp: number }`.
2. Melakukan verifikasi tanda tangan EIP-712 typed data di server menggunakan pustaka `viem` (`verifyTypedData`):
   - Domain: `{ name: "OMEN", version: "1", chainId, verifyingContract: factoryAddress }`
   - PrimaryType: `"BeliefConfirmation"`
   - Types: `BeliefConfirmation: [{ name: "beliefId", type: "string" }, { name: "statement", type: "string" }, { name: "timestamp", type: "uint256" }]`
3. Memastikan alamat penandatangan (`recoveredAddress`) cocok dengan alamat kreator yang terdaftar atau author terverifikasi di `belief_sources`.
4. Mengubah status keyakinan pada tabel `beliefs` menjadi `CONFIRMED`.
5. Menyimpan audit log tanda tangan ke tabel `creator_confirmations`.
6. Memperbarui reputasi kreator pada tabel `creator_profiles` (`confirmed_beliefs = confirmed_beliefs + 1`).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/app/api/beliefs/[id]/confirm/route.ts` untuk `POST /api/beliefs/[id]/confirm`.
- [x] Memverifikasi EIP-712 Typed Data Signature secara ketat dengan `viem`.
- [x] Menolak permintaan dengan tanda tangan tidak valid, expired timestamp, atau signer address yang tidak sesuai (HTTP 401/403).
- [x] Memperbarui status belief menjadi `CONFIRMED` dan mengupdate metrik profil kreator.
- [x] Menyusun unit test pada `omen/web/tests/api-creator-confirm.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/[id]/confirm/route.ts`
- `omen/web/lib/eip712/confirmation.ts`
- `omen/web/tests/api-creator-confirm.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyusun unit test TDD pada `omen/web/tests/api-creator-confirm.test.ts` yang mencakup verifikasi zero-comment, verifikasi sukses signature EIP-712 viem, validasi signer address mismatch (HTTP 401), penanganan missing belief (HTTP 404), dan missing required body fields (HTTP 400).
  2. Mengembangkan helper `omen/web/lib/eip712/confirmation.ts` dengan fungsi `verifyBeliefConfirmationSignature` menggunakan `verifyTypedData` dari `viem`.
  3. Mengembangkan route handler `POST /api/beliefs/[id]/confirm` pada `omen/web/app/api/beliefs/[id]/confirm/route.ts` dengan update status belief ke `CONFIRMED`, logging ke `creator_confirmations`, serta update/upsert ke `creator_profiles`.
  4. Menjalankan pengujian unit test dan verifikasi linter/tipe TypeScript (100% pass, 0 lint error, 0 comment).
- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/eip712/confirmation.ts`
  - `omen/web/app/api/beliefs/[id]/confirm/route.ts`
  - `omen/web/tests/api-creator-confirm.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan standardisasi EIP-712 Typed Data Domain (`{ name: "OMEN", version: "1", chainId }`) dengan struktur tipe data `BeliefConfirmation: [{ name: "beliefId", type: "string" }, { name: "statement", type: "string" }, { name: "timestamp", type: "uint256" }]` untuk kompatibilitas off-chain wallet signature di Web3.
