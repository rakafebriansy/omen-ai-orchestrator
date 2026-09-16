---
id: TICKET-69
title: Implementasi Smart Contract OmenMarket.sol
status: Todo
priority: High
labels: [SmartContract, Foundry, Solidity, Market]
---

# Deskripsi
`OmenMarket.sol` adalah kontrak *escrow & settlement* individual untuk satu pasar keyakinan. Kontrak ini mengelola siklus hidup pasar dari `OPEN`, `CLOSED`, `RESOLVED`, hingga `SETTLED` (atau `VOID`).

Prinsip dan aturan ketat arsitektur V1:
1. **Posisi Biner Keyakinan:** Mendukung penyetoran Native ETH untuk posisi `depositAgree()` dan `depositDisagree()`. Penyetoran hanya diizinkan saat status `OPEN` dan sebelum `closeTime`.
2. **Pola Penarikan Aman (Pull Over Push):** Pemenang mengklaim bagian hadiah sendiri melalui fungsi `claimPayout()`.
3. **Formula Pembagian Pool:** Payout dihitung proporsional `(userStake / winningPool) * distributablePool`.
4. **Proteksi & Keamanan:** Menggunakan `ReentrancyGuard`, `Pausable`, Checks-Effects-Interactions pattern, dan mapping `hasClaimed[wallet]` untuk mencegah double-spending/double-claim.
5. **Penanganan Kasus Ekstrem & VOID:** Jika status `VOID` (oracle gagal atau pembatalan darurat), seluruh partisipan dapat menarik 100% dana pokok mereka secara proporsional.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan `OmenMarket.sol` di `omen/contracts/src/OmenMarket.sol`.
- [ ] Menyediakan fungsi `depositAgree()` dan `depositDisagree()` dengan payable Native ETH.
- [ ] Menyediakan fungsi `resolveMarket(Outcome outcome)` yang hanya dapat dipanggil oleh Resolver role atau Factory setelah `closeTime`.
- [ ] Menyediakan fungsi `claimPayout()` dengan kalkulasi proporsional pool share dan proteksi `hasClaimed`.
- [ ] Menyediakan fungsi `voidMarket()` untuk penanganan darurat/oracle failure yang mengizinkan penarikan refund penuh.
- [ ] Memancarkan events: `PositionTaken`, `MarketClosed`, `MarketResolved`, `PayoutClaimed`, `MarketVoided`.
- [ ] Mematuhi Zero-Comment Policy dan lulus kompilasi `forge build` 100%.

## Target Lingkup File (Affected Files)
- `omen/contracts/src/OmenMarket.sol`
- `omen/contracts/src/interfaces/IOmenMarket.sol`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
