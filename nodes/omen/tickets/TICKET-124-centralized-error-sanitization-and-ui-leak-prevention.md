---
id: TICKET-124
title: Centralized Error Sanitization and UI Raw Error Leak Elimination
status: Done
priority: High
labels: [Frontend, UI/UX, Security, ErrorHandling]
---

# Deskripsi
Terdapat kebocoran teknis (*information leak*) pada antarmuka pengguna di mana pesan error mentah (*raw error stack traces*, calldata hex EVM, dan dump JSON-RPC seperti `The total cost (gas * gas fee + value) of executing this transaction exceeds the balance... Request Arguments: from: 0x9124...`) ditampilkan langsung di dalam elemen alert UI (`<div role="alert">`). Hal ini merusak estetika antarmuka, menurunkan *user experience*, dan berpotensi mengekspos detail teknis internal yang membingungkan pengguna akhir.

Tiket ini membangun modul sanitasi error terpusat (`web/lib/format-error.ts`) dengan helper `formatUserErrorMessage()` yang memetakan error teknis (insufficient funds, user rejected transaction, network timeout, rate limits) menjadi pesan ramah pengguna yang bersih, sembari mencatat seluruh *raw error stack* secara lengkap dan eksklusif ke `console.error` untuk kebutuhan debugging developer.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Membuat modul utilitas `web/lib/format-error.ts` dengan fungsi `formatUserErrorMessage(error, defaultFallback)`.
- [x] Memetakan pola error umum Web3 dan REST API (insufficient funds, user rejected, contract execution revert, JSON RPC parse errors, 429 rate limit) ke deskripsi ramah pengguna.
- [x] Memastikan `console.error("[Omen Client Error]", error)` selalu dieksekusi untuk logging developer di konsol browser.
- [x] Mengganti seluruh binding state `error: err.message` mentah di komponen:
  - `web/components/BeliefSubmitForm.tsx`
  - `web/components/AdminMarketCreateForm.tsx`
  - `web/components/CreatorConfirmation.tsx`
  - `web/components/MarketDetailPanels.tsx`
  - `web/app/api/beliefs/submit/route.ts`
- [x] Memverifikasi bahwa tidak ada raw stack trace atau calldata hex yang lolos ke antarmuka pengguna pada skenario error apa pun.

## Target Lingkup File (Affected Files)
- `omen/web/lib/format-error.ts`
- `omen/web/components/BeliefSubmitForm.tsx`
- `omen/web/components/AdminMarketCreateForm.tsx`
- `omen/web/components/CreatorConfirmation.tsx`
- `omen/web/components/MarketDetailPanels.tsx`
- `omen/web/app/api/beliefs/submit/route.ts`

---

## AI Execution Log dan Output

- **Langkah Teknis Tereksekusi:**
  1. Membuat `web/lib/format-error.ts` dengan pattern matching komprehensif terhadap `insufficient funds`, `user rejected`, `execution reverted`, `rate limit`, `429`, `failed to fetch`, dan parameterisasi fallback.
  2. Memperbarui `BeliefSubmitForm.tsx` saat submit dan ekstraksi belief gagal agar menampilkan pesan terformat.
  3. Memperbarui `AdminMarketCreateForm.tsx`, `CreatorConfirmation.tsx`, dan `MarketDetailPanels.tsx` untuk menggunakan `formatUserErrorMessage`.
  4. Mengisolasi `console.error` sehingga developer tetap memiliki full stack trace di browser devtools tanpa mencemari alert visual.
  5. Menjalankan pengujian regresi UI dan validasi error state.

- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/format-error.ts`
  - `omen/web/components/BeliefSubmitForm.tsx`
  - `omen/web/components/AdminMarketCreateForm.tsx`
  - `omen/web/components/CreatorConfirmation.tsx`
  - `omen/web/components/MarketDetailPanels.tsx`
  - `omen/web/app/api/beliefs/submit/route.ts`

- **Catatan dan Keputusan Arsitektural:**
  - Prinsip pemisahan *User-Facing Feedback* (Clean & Actionable) vs *Developer Observability* (Console Stacks) diterapkan secara konsisten di seluruh lapisan interaksi frontend.
