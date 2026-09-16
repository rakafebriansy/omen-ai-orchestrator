---
id: TICKET-100
title: Konfigurasi Environment Variables Lengkap & Verifikasi Trust Checklist Peluncuran Publik
status: Todo
priority: High
labels: [DevOps, Security, Documentation, Configuration]
---

# Deskripsi
Tiket penutup arsitektur OMEN V1 ini bertujuan mendokumentasikan seluruh konfigurasi environment variables yang dibutuhkan untuk deployment produksi / live staging serta melakukan audit verifikasi kepatuhan terhadap **Trust Checklist** sebelum peluncuran publik.

Cakupan Variabel Lingkungan:
```env
NEXT_PUBLIC_CHAIN_ENV=testnet
NEXT_PUBLIC_ETH_SEPOLIA_RPC=https://eth-sepolia.g.alchemy.com/v2/...
NEXT_PUBLIC_ROBINHOOD_TESTNET_RPC=https://rpc.testnet.chain.robinhood.com
NEXT_PUBLIC_ROBINHOOD_CHAIN_ID=46630
NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA=0x...
NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_ROBINHOOD=0x...
NEXT_PUBLIC_CHAINLINK_ETH_USD_FEED=0x...
NEXT_PUBLIC_CHAINLINK_BTC_USD_FEED=0x...
NEXT_PUBLIC_CHAINLINK_SOL_USD_FEED=0x...
AI_API_KEY=...
AI_MODEL=meta-llama/llama-3.3-70b-instruct:free
ADMIN_PRIVATE_KEY=... # Server-side only
```

Item Trust Checklist yang diverifikasi:
1. Smart contract `OmenFactory` dan `OmenMarket` terverifikasi di Etherscan Sepolia dan Blockscout Robinhood.
2. Tidak ada private key, service role key, atau secret yang terekspos di client bundle (`NEXT_PUBLIC_`).
3. Seluruh endpoint API terproteksi validasi Zod dan otorisasi yang ketat.
4. UI mempertahankan tema OpenZeppelin dark mode secara konsisten dan responsif di seluruh breakpoint perangkat.
5. README proyek memuat instruksi instalasi, arsitektur, dan panduan kontribusi yang komprehensif.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Memperbarui `omen/web/.env.example` dan `omen/contracts/.env.example` dengan seluruh variabel lingkungan V1.
- [ ] Menyusun dokumentasi arsitektur dan panduan menjalankan proyek pada `omen/web/README.md`.
- [ ] Memastikan tidak ada secret/API key yang terekspos ke bundle browser client (`NEXT_PUBLIC_`).
- [ ] Memverifikasi kelulusan 100% build Next.js (`npm run build`), TypeScript typecheck (`tsc --noEmit`), dan seluruh test suite Vitest.
- [ ] Mematuhi Zero-Comment Policy pada seluruh codebase.

## Target Lingkup File (Affected Files)
- `omen/web/.env.example`
- `omen/contracts/.env.example`
- `omen/web/README.md`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
