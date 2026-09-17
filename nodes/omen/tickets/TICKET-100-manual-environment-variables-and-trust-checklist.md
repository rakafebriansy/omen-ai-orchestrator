---
id: TICKET-100
title: (MANUAL) Penyediaan Kredensial Environment Variables & Verifikasi Trust Checklist Peluncuran Publik
status: Todo
priority: High
labels: [DevOps, Security, Documentation, Configuration, ManualAction]
---

# Deskripsi
Tiket penutup arsitektur OMEN V1 ini bertujuan mendokumentasikan seluruh konfigurasi environment variables yang dibutuhkan untuk deployment live / public testnet serta melakukan verifikasi kepatuhan terhadap **Trust Checklist** sebelum peluncuran publik.

Tiket ini mencakup penyusunan template `.env.example` dan dokumentasi arsitektur di `README.md` oleh AI, pengisian kredensial API keys dan private key oleh Developer di `.env.local`, serta audit verifikasi menyeluruh.

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
- [ ] AI Agent memperbarui `omen/web/.env.example` dan `omen/contracts/.env.example` dengan seluruh variabel lingkungan V1.
- [ ] AI Agent menyusun dokumentasi arsitektur dan panduan menjalankan proyek pada `omen/web/README.md`.
- [ ] **(Manual Developer)** Developer mengisi kredensial nyata (`AI_API_KEY` OpenRouter, `ADMIN_PRIVATE_KEY`, RPC URLs) pada `omen/web/.env.local`.
- [ ] Memastikan tidak ada secret/API key yang terekspos ke bundle browser client (`NEXT_PUBLIC_`).
- [ ] Memverifikasi kelulusan 100% build Next.js (`npm run build`), TypeScript typecheck (`tsc --noEmit`), dan seluruh test suite Vitest.
- [ ] Mematuhi Zero-Comment Policy pada seluruh codebase.

## Target Lingkup File (Affected Files)
- `omen/web/.env.example`
- `omen/contracts/.env.example`
- `omen/web/.env.local`
- `omen/web/README.md`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
