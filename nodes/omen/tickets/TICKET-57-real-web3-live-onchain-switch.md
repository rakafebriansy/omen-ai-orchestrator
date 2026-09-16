---
id: TICKET-57
title: Real On-Chain Contract Wiring (Switch Mock Engine ke Live Arbitrum Sepolia)
status: Todo
priority: High
labels: [Frontend, Web3, SmartContract, LiveOnChain, Integration]
---

# Deskripsi
Mengalihkan seluruh transaksi taruhan (`usePlaceBet`), klaim kemenangan (`useClaimPayout`), serta aksi admin (`useAdminCreateMarket`, `useAdminResolveMarket`) dari simulator in-memory ke smart contract live `PredictionMarket.sol` di blockchain Arbitrum Sepolia, serta menjalankan validasi menyeluruh end-to-end dengan dompet terhubung.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengubah variabel lingkungan `NEXT_PUBLIC_USE_MOCK_CONTRACT="false"`.
- [ ] Memastikan `usePlaceBet` mengirimkan transaksi on-chain nyata dan memicu popup konfirmasi di dompet pengguna.
- [ ] Memastikan `useClaimPayout` mengeksekusi klaim Native ETH langsung dari pool likuiditas smart contract.
- [ ] Memastikan `useAdminCreateMarket` dan `useAdminResolveMarket` mengeksekusi mutasi on-chain terproteksi `onlyOwner`.

## Target Lingkup File (Affected Files)
- `omen/web/.env.local`
- `omen/web/hooks/usePlaceBet.ts`
- `omen/web/hooks/useClaimPayout.ts`
- `omen/web/hooks/useAdminCreateMarket.ts`
- `omen/web/hooks/useAdminResolveMarket.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Draf tiket switch live on-chain dibuat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/.env.local`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Penyelesaian tiket ini menandai kesiapan penuh platform Omen di jaringan testnet Arbitrum Sepolia sebelum rilis produksi.
