---
id: TICKET-94
title: Pembuatan Web3 Wagmi Hook (useCreateMarket untuk OmenFactory)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/hooks/useCreateMarket.ts`.
- [ ] Mendekode event log `MarketCreated` untuk mengekstrak alamat kontrak pasar baru secara otomatis.
- [ ] Menyediakan penanganan error yang ramah pengguna jika wallet menolak transaksi atau jaringan tidak cocok.
- [ ] Menyusun unit test pada `omen/web/tests/use-create-market.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/hooks/useCreateMarket.ts`
- `omen/web/tests/use-create-market.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
