---
id: TICKET-69
title: Implementasi Smart Contract OmenMarket.sol
status: Done
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
- [x] Mengimplementasikan `OmenMarket.sol` di `omen/contracts/src/OmenMarket.sol`.
- [x] Menyediakan fungsi `depositAgree()` dan `depositDisagree()` dengan payable Native ETH.
- [x] Menyediakan fungsi `resolveMarket(Outcome outcome)` yang hanya dapat dipanggil oleh Resolver role atau Factory setelah `closeTime`.
- [x] Menyediakan fungsi `claimPayout()` dengan kalkulasi proporsional pool share dan proteksi `hasClaimed`.
- [x] Menyediakan fungsi `voidMarket()` untuk penanganan darurat/oracle failure yang mengizinkan penarikan refund penuh.
- [x] Memancarkan events: `PositionTaken`, `MarketClosed`, `MarketResolved`, `PayoutClaimed`, `MarketVoided`.
- [x] Mematuhi Zero-Comment Policy dan lulus kompilasi `forge build` 100%.

## Target Lingkup File (Affected Files)
- `omen/contracts/src/OmenMarket.sol`
- `omen/contracts/src/interfaces/IOmenMarket.sol`
- `omen/contracts/test/OmenMarket.t.sol`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis Foundry unit testing suite mendalam di `omen/contracts/test/OmenMarket.t.sol` (12 skenario pengujian komprehensif: setoran biner, validasi timing `closeTime`, penolakan `0 ETH`, otorisasi resolver/admin, kalkulasi proporsional payout, proteksi double-claim, skenario refund 100% `VOID`, dan darurat `pause`/`unpause`).
  2. Mengimplementasikan kontrak `OmenMarket.sol` yang mewarisi `ReentrancyGuard` dan `Pausable` OpenZeppelin, mendukung otorisasi peran dinamis via `OmenFactory` (`RESOLVER_ROLE` / `DEFAULT_ADMIN_ROLE`).
  3. Memvalidasi emisi event `PositionTaken`, `MarketResolved`, `PayoutClaimed`, `MarketVoided`.
  4. Menjalankan `forge test --match-contract OmenMarketTest -vv` dengan 12 test lulus 100%.
  5. Menjalankan seluruh test suite Foundry (20 total tests across 3 suites) dengan 100% PASS.
- **Ringkasan File Terpengaruh:**
  - `omen/contracts/src/OmenMarket.sol` (Implementasi smart contract individual market settlement & escrow)
  - `omen/contracts/src/interfaces/IOmenMarket.sol` (Antarmuka publik IOmenMarket)
  - `omen/contracts/test/OmenMarket.t.sol` (Foundry test suite komprehensif untuk OmenMarket)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan pola Pull Claim (user menarik sendiri payout) untuk mencegah kegagalan DoS gas limit pada penyelesaian massal.
  - Otorisasi fungsi `resolveMarket` dan `voidMarket` terintegrasi langsung dengan RBAC di `OmenFactory` (`RESOLVER_ROLE` & `DEFAULT_ADMIN_ROLE`).
  - Zero-Comment Policy ditegakkan 100% pada seluruh berkas Solidity.
