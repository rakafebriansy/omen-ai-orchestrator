---
id: TICKET-108
title: Harmonize Belief Submission & EIP-712 Creator Confirmation Payloads
status: Done
priority: High
labels: [Frontend, Backend, BFF, Beliefs, EIP712, Supabase]
---

# Deskripsi
Harmonisasi format payload antara Frontend (`BeliefSubmitForm.tsx`, `useCreateMarket.ts`, `useCreatorConfirm.ts`) dan Backend Route Handlers (`/api/beliefs/submit`, `/api/beliefs/[id]/confirm`). Memastikan `POST /api/beliefs/submit` dapat menangani submission baru dari ekstraksi AI (nested `extracted` object atau flat properties) serta pembaruan pasar on-chain dari `useCreateMarket`. Selain itu, memastikan `POST /api/beliefs/[id]/confirm` menerima format `creator_address` dan `creator` serta timestamp yang valid untuk verifikasi tanda tangan EIP-712.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `web/app/api/beliefs/submit/route.ts` mendukung payload ekstraksi AI dari `BeliefSubmitForm` (`extracted.statement`, `rawText`, `authorHandle`, `sourceUrl`).
- [x] `web/app/api/beliefs/submit/route.ts` mendukung pembaruan tautan on-chain dari `useCreateMarket` (`beliefId`, `marketAddress`, `txHash`).
- [x] `web/app/api/beliefs/submit/route.ts` mengembalikan `marketId` di root response dan `data: { belief_id, market_id, ... }`.
- [x] `web/components/BeliefSubmitForm.tsx` mengirimkan payload lengkap dan membaca ID pasar hasil deploy dengan benar.
- [x] `web/app/api/beliefs/[id]/confirm/route.ts` mendukung parameter `creator_address`, `creator`, `signature`, `timestamp`, dan `chain_id`.
- [x] `web/hooks/useCreatorConfirm.ts` mengirimkan `creator_address`, `creator`, `signature`, `timestamp`, dan `chain_id`.
- [x] Seluruh unit test beliefs dan konfirmasi EIP-712 lulus tanpa regresi.

## Target Lingkup File (Affected Files)
- `web/app/api/beliefs/submit/route.ts`
- `web/components/BeliefSubmitForm.tsx`
- `web/hooks/useCreateMarket.ts`
- `web/app/api/beliefs/[id]/confirm/route.ts`
- `web/hooks/useCreatorConfirm.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memperluas fleksibilitas parser body pada `web/app/api/beliefs/submit/route.ts` untuk menangani form submission maupun on-chain market update.
  2. Menyelaraskan form submission di `web/components/BeliefSubmitForm.tsx`.
  3. Memperbarui `web/app/api/beliefs/[id]/confirm/route.ts` agar mendukung multi-key payload (`creator_address` / `creator`).
  4. Menyelaraskan pengiriman payload pada `web/hooks/useCreatorConfirm.ts`.
  5. Memverifikasi seluruh acceptance criteria lulus pada pengujian otomatis vitest.
- **Ringkasan File Terpengaruh:**
  - `web/app/api/beliefs/submit/route.ts`
  - `web/components/BeliefSubmitForm.tsx`
  - `web/hooks/useCreateMarket.ts`
  - `web/app/api/beliefs/[id]/confirm/route.ts`
  - `web/hooks/useCreatorConfirm.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Standardisasi response envelope pada rute beliefs memastikan UI selalu mendapatkan `marketId` tanpa fallback dummy.
