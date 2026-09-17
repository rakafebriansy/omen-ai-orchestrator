---
id: TICKET-97
title: Pembuatan Komponen & Hook Konfirmasi Kreator EIP-712 (CreatorConfirmation UI)
status: Done
priority: Medium
labels: [Frontend, UI, Web3, EIP712]
---

# Deskripsi
Tiket ini menyediakan antarmuka bagi para kreator/pembuat opini untuk menandatangani dan memvalidasi keyakinan mereka secara resmi melalui standar kriptografis EIP-712 Typed Data Signing tanpa biaya gas (*gasless*).

Komponen & Fitur:
1. `CreatorConfirmation.tsx`:
   - Modal atau banner cerdas yang muncul saat seorang pengguna terhubung dengan dompet yang cocok dengan alamat kreator yang terdaftar pada sebuah belief berstatus `DETECTED`.
   - Menampilkan cuplikan pernyataan belief dan tombol "Confirm Belief Official".
   - Tombol memicu tanda tangan EIP-712 via Wagmi `useSignTypedData`.
   - Mengirim signature ke `POST /api/beliefs/[id]/confirm`.
   - Memperbarui badge dari `AI DETECTED` menjadi `✓ CONFIRMED BY @handle` dengan efek animasi transisi yang mulus.
2. `useCreatorConfirm.ts`:
   - Custom React hook yang merangkum pembuatan Typed Data, request wallet signature, pengiriman payload ke server, dan state handling (`isSigning`, `isConfirming`, `isSuccess`, `error`).

> 🎨 **UI Style Preservation Note:**
> Desain banner/modal konfirmasi, tombol tanda tangan dengan highlight ungu/emas, lencana resmi `✓ CONFIRMED`, efek shimmer dan popup konfirmasi **WAJIB MENGIKUTI** tema visual OpenZeppelin dark mode dan styling Tailwind yang sudah ada di OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/components/CreatorConfirmation.tsx` dan `omen/web/hooks/useCreatorConfirm.ts`.
- [x] Mengonfigurasi skema EIP-712 typed data (`domain`, `types`, `primaryType`, `message`) yang kompatibel dengan standar ERC-712.
- [x] Menangani transisi visual status badge secara reaktif setelah tanda tangan berhasil diverifikasi server.
- [x] Menyediakan penanganan penolakan tanda tangan oleh user (*user rejected signature*) secara elegan.
- [x] Mempertahankan style UI, tema dark mode, dan responsivitas komponen.
- [x] Menyusun unit test pada `omen/web/tests/creator-confirmation.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/CreatorConfirmation.tsx`
- `omen/web/hooks/useCreatorConfirm.ts`
- `omen/web/tests/creator-confirmation.test.tsx`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Mengembangkan `hooks/useCreatorConfirm.ts` dengan skema EIP-712 typed data (`ConfirmBelief`), penandatanganan gasless via Wagmi `useSignTypedData`, dev mock mode simulation, dan auto-sync ke `/api/beliefs/[id]/confirm`.
  2. Mengembangkan komponen `components/CreatorConfirmation.tsx` dengan banner bertema OpenZeppelin dark mode, validasi pembuat opini asli, spinner state, dan status badge `EIP-712 Authenticated`.
  3. Menyusun unit test suite `tests/creator-confirmation.test.tsx` memvalidasi pemanggilan hook, rendering komponen, transisi tanda tangan, dan callback handler.
  4. Memvalidasi 3/3 test lulus 100% pada Vitest dan ESLint dengan kepatuhan penuh Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `web/hooks/useCreatorConfirm.ts`
  - `web/components/CreatorConfirmation.tsx`
  - `web/tests/creator-confirmation.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengisolasi mock signature untuk unit testing lingkungan browser tanpa memerlukan ekstensi dompet nyata.
