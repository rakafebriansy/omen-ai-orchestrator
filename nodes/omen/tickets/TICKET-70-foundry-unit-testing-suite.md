---
id: TICKET-70
title: Foundry Unit & Invariant Testing Suite untuk OmenFactory dan OmenMarket
status: Todo
priority: High
labels: [SmartContract, Foundry, Testing]
---

# Deskripsi
Keandalan dan keamanan smart contract OMEN V1 wajib dibuktikan melalui suite pengujian Foundry yang komprehensif, mencakup unit testing, branch coverage, edge cases, serta fuzz testing.

Skenario uji minimal yang wajib diuji:
1. Pembuatan pasar oleh Factory dan penolakan konfigurasi invalid.
2. Penyetoran AGREE/DISAGREE dalam rentang `openTime` hingga `closeTime`.
3. Penolakan penyetoran setelah `closeTime` terlewati.
4. Resolusi pasar oleh Resolver setelah deadline (AGREE_WON, DISAGREE_WON).
5. Klaim payout oleh pihak pemenang dengan verifikasi penambahan saldo ETH yang presisi.
6. Penolakan klaim oleh pihak yang kalah dan pencegahan klaim ganda (*double claim*).
7. Pembatalan pasar (VOID) dan verifikasi refund 100% untuk semua partisipan.
8. Penanganan kondisi satu sisi pool bernilai nol (*zero opposing pool*).
9. Verifikasi bahwa Admin/Resolver tidak dapat mencuri atau menarik pool di luar aturan kontrak.
10. Proteksi `Pausable` dan `ReentrancyGuard`.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyusun file test `omen/contracts/test/OmenFactory.t.sol` untuk validasi fungsi factory, role control, dan indexing.
- [ ] Menyusun file test `omen/contracts/test/OmenMarket.t.sol` untuk validasi siklus penuh deposit, resolusi, klaim, void, dan invariant pools.
- [ ] Menyusun fuzz tests dengan input acak amount dan timestamp untuk menguji ketahanan matematika overflow/underflow.
- [ ] Eksekusi `forge test --gas-report` lulus 100% dengan 0 kegagalan.
- [ ] Mematuhi Zero-Comment Policy pada seluruh file pengujian Solidity.

## Target Lingkup File (Affected Files)
- `omen/contracts/test/OmenFactory.t.sol`
- `omen/contracts/test/OmenMarket.t.sol`
- `omen/contracts/test/helpers/TestHelpers.sol`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
