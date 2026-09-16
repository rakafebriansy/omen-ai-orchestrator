---
id: TICKET-99
title: Validasi Siklus Hidup Penuh End-to-End pada Dual Testnet (Sepolia & Robinhood Chain)
status: Todo
priority: High
labels: [Testing, E2E, Web3, MultiChain]
---

# Deskripsi
Tiket ini menyusun dan mengeksekusi rangkaian pengujian End-to-End (E2E) otomatis untuk memvalidasi siklus hidup penuh (*full lifecycle*) protokol OMEN V1 di kedua jaringan (Ethereum Sepolia dan Robinhood Chain Testnet).

Siklus hidup yang diverifikasi:
1. **Penciptaan Belief & Pasar**: Input teks opini -> Ekstraksi AI terstruktur -> Konfirmasi -> Pembuatan kontrak pasar `OmenMarket` via `OmenFactory`.
2. **Penempatan Posisi (Trading)**:
   - Pengguna A: Connect Wallet -> Menyetor posisi `AGREE` dengan ETH.
   - Pengguna B: Connect Wallet -> Menyetor posisi `DISAGREE` dengan ETH.
   - Verifikasi pembaruan pool dan penghitungan rasio konsensus.
3. **Konfirmasi Kreator (EIP-712)**: Kreator melakukan sign typed data -> Status keyakinan berubah menjadi `CONFIRMED`.
4. **Penyelesaian Pasar (Resolution Engine)**: Deadline tercapai -> Pengambilan snapshot harga Chainlink -> Eksekusi fungsi `resolveMarket` on-chain.
5. **Klaim Kemenangan (Settlement)**: Pengguna pemenang memanggil `claimPayout()` -> Penambahan saldo ETH berhasil terverifikasi.
6. **Verifikasi Kasus Batal (VOID)**: Skenario kegagalan data oracle menghasilkan penarikan refund penuh 100%.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menyusun test suite E2E komprehensif pada `omen/web/tests/e2e/belief-market-cycle.test.tsx`.
- [ ] Memvalidasi seluruh transisi state dari `OPEN`, `CLOSED`, `RESOLVED`, hingga `SETTLED` dan `VOID`.
- [ ] Memvalidasi kalkulasi payout proporsional dan proteksi pencegahan klaim ganda.
- [ ] Memastikan seluruh rangkaian test berjalan mulus dan lulus 100% pada lingkungan Vitest.
- [ ] Mematuhi Zero-Comment Policy pada seluruh file pengujian.

## Target Lingkup File (Affected Files)
- `omen/web/tests/e2e/belief-market-cycle.test.tsx`
- `omen/web/tests/e2e/dual-chain-workflow.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
