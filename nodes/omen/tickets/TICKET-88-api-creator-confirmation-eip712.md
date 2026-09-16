---
id: TICKET-88
title: Pembuatan API Route Konfirmasi Kreator EIP-712 (POST /api/beliefs/[id]/confirm)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/app/api/beliefs/[id]/confirm/route.ts` untuk `POST /api/beliefs/[id]/confirm`.
- [ ] Memverifikasi EIP-712 Typed Data Signature secara ketat dengan `viem`.
- [ ] Menolak permintaan dengan tanda tangan tidak valid, expired timestamp, atau signer address yang tidak sesuai (HTTP 401/403).
- [ ] Memperbarui status belief menjadi `CONFIRMED` dan mengupdate metrik profil kreator.
- [ ] Menyusun unit test pada `omen/web/tests/api-creator-confirm.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/[id]/confirm/route.ts`
- `omen/web/lib/eip712/confirmation.ts`
- `omen/web/tests/api-creator-confirm.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
