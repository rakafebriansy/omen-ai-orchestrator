---
id: TICKET-97
title: Pembuatan Komponen & Hook Konfirmasi Kreator EIP-712 (CreatorConfirmation UI)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/components/CreatorConfirmation.tsx` dan `omen/web/hooks/useCreatorConfirm.ts`.
- [ ] Mengonfigurasi skema EIP-712 typed data (`domain`, `types`, `primaryType`, `message`) yang kompatibel dengan standar ERC-712.
- [ ] Menangani transisi visual status badge secara reaktif setelah tanda tangan berhasil diverifikasi server.
- [ ] Menyediakan penanganan penolakan tanda tangan oleh user (*user rejected signature*) secara elegan.
- [ ] Mempertahankan style UI, tema dark mode, dan responsivitas komponen.
- [ ] Menyusun unit test pada `omen/web/tests/creator-confirmation.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/components/CreatorConfirmation.tsx`
- `omen/web/hooks/useCreatorConfirm.ts`
- `omen/web/tests/creator-confirmation.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
