---
id: TICKET-37
title: Unit Testing Hardhat PredictionMarket.sol
status: Todo
priority: High
labels: [SmartContract, Testing]
---

# Deskripsi
Membangun rangkaian pengujian unit test Hardhat komprehensif di `omen/contracts/test/PredictionMarket.test.ts` untuk memverifikasi matematika odds, distribusi pool, keamanan reentrancy, dan penanganan kasus batas.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Skenario Test Suite
1. Pembuatan pasar sukses dan penolakan jika dipanggil non-owner.
2. Pemasangan taruhan Yes dan No dengan nominal ETH yang sesuai.
3. Penolakan taruhan jika batas deadline telah lewat.
4. Resolusi pasar Yes dan klaim payout proporsional bagi pemenang Yes.
5. Resolusi pasar No dan klaim payout proporsional bagi pemenang No.
6. Pencegahan klaim ganda oleh akun yang sama.
7. Pembatalan pasar (cancelMarket) dan penarikan refund 100%.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Seluruh skenario unit test lulus 100% tanpa kegagalan.
- [ ] Pengujian mencakup proteksi akses unauthorized non-owner.
- [ ] Pengujian memvalidasi keakuratan saldo transfer payout Native ETH.

## Target Lingkup File (Affected Files)
- `omen/contracts/test/PredictionMarket.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
