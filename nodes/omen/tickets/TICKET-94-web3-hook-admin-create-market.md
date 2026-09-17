---
id: TICKET-94
title: Pembuatan Web3 Wagmi Hook (useCreateMarket untuk OmenFactory)
status: Done
priority: Medium
labels: [Frontend, Web3, Hooks, Factory]
---

# Deskripsi
Tiket ini membangun custom React hook `useCreateMarket` untuk memfasilitasi pembuatan pasar baru melalui interaksi frontend langsung ke smart contract `OmenFactory.sol` bagi pengguna yang memiliki hak/role pembuat pasar atau alur verifikasi on-chain.

Fitur hook:
1. Memanggil fungsi `OmenFactory.createMarket(beliefHash, sourceHash, resolutionHash, openTime, closeTime, resolutionConfig)`.
2. Menghitung hash parameter input di sisi klien jika belum di-generate oleh backend.
3. Mendekode receipt transaksi untuk mengekstrak alamat kontrak `OmenMarket` yang baru di-deploy dari event `MarketCreated`.
4. Mengembalikan state eksekusi: `createMarketAsync`, `isPending`, `isDeploying`, `marketAddress`, `error`.

> 🎨 **UI Style Preservation Note:**
> Tampilan form pembuatan pasar, dialog status deployment, animasi loading progress bar, dan tombol submit on-chain **WAJIB MEMPERTAHANKAN** tema visual OpenZeppelin dark mode dan styling Tailwind yang konsisten.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/hooks/useCreateMarket.ts`.
- [x] Mendekode event log `MarketCreated` untuk mengekstrak alamat kontrak pasar baru secara otomatis.
- [x] Menyediakan penanganan error yang ramah pengguna jika wallet menolak transaksi atau jaringan tidak cocok.
- [x] Menyusun unit test pada `omen/web/tests/use-create-market.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useCreateMarket.ts`
- `omen/web/tests/use-create-market.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menambahkan `OMEN_FACTORY_ADDRESS` dan event `MarketCreated` pada `lib/contracts.ts`.
  2. Mengimplementasikan `useCreateMarket.ts` yang menangani pembuatan pasar via `writeContractAsync` ke `OmenFactory.sol` serta simulasi dev mode (`USE_MOCK_CONTRACT`) dengan sinkronisasi otomatis ke `/api/beliefs/submit`.
  3. Menyusun unit test suite `tests/use-create-market.test.ts` memverifikasi inisialisasi state, eksekusi pemanggilan on-chain/mock, dan mekanisme reset status.
  4. Memvalidasi 3/3 test lulus 100% pada Vitest dan ESLint dengan Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `web/lib/contracts.ts`
  - `web/hooks/useCreateMarket.ts`
  - `web/tests/use-create-market.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menyediakan fallback address creator dan oracle price feed default untuk kemudahan testing dan eksekusi instan.
