---
id: TICKET-36
title: Implementasi Smart Contract PredictionMarket.sol
status: Todo
priority: High
labels: [SmartContract, Solidity]
---

# Deskripsi
Mengembangkan smart contract PredictionMarket.sol mewarisi Ownable dan ReentrancyGuard dengan fungsi createMarket, placeBet, resolveMarket, claim, dan cancelMarket.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Fungsi createMarket hanya dapat diakses oleh owner kontrak.
- [ ] Fungsi placeBet menerima Native ETH dan memvalidasi batas waktu deadline.
- [ ] Fungsi claim membagikan payout proporsional secara nonReentrant.
- [ ] Kompilasi Solidity 0.8.20 berhasil tanpa peringatan.

## Target Lingkup File (Affected Files)
- `omen/contracts/contracts/PredictionMarket.sol`

---

## AI Execution Log & Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan & Keputusan Arsitektural (Jika Ada):**
