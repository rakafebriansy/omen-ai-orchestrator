---
id: TICKET-38
title: Script Deployment Testnet dan Ekspor ABI
status: Todo
priority: High
labels: [SmartContract, DevOps]
---

# Deskripsi
Membuat script deployment di `omen/contracts/scripts/deploy.ts` untuk mendeploy kontrak ke Arbitrum Sepolia dan mengekspor alamat kontrak beserta ABI ke frontend `omen/web/lib/contracts.ts`.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Deployment Script
- Script `scripts/deploy.ts` mendeploy `PredictionMarket.sol` menggunakan signer deployer.
- Script menuliskan alamat kontrak aktif dan file ABI JSON ke `omen/web/lib/contracts.ts`.
- Menyertakan instruksi verifikasi kontrak di block explorer Arbiscan Sepolia.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Script deploy.ts berhasil mengeksekusi migrasi kontrak ke testnet.
- [ ] Berkas omen/web/lib/contracts.ts memuat ABI final dan alamat kontrak aktif.
- [ ] Dokumentasi deployment testnet tercatat di README.

## Target Lingkup File (Affected Files)
- `omen/contracts/scripts/deploy.ts`
- `omen/web/lib/contracts.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
