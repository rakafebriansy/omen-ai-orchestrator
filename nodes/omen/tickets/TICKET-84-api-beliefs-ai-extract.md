---
id: TICKET-84
title: Pembuatan API Route Ekstraksi AI Terstruktur (POST /api/beliefs/extract)
status: Done
priority: High
labels: [Backend, API, AI, OpenRouter, Zod]
---

# Deskripsi
Tiket ini membangun serverless endpoint `POST /api/beliefs/extract` yang memanfaatkan LLM (via OpenRouter API dengan model open-source/gratis seperti Meta Llama 3 / Mistral) untuk mengurai postingan teks mentah menjadi objek JSON terstruktur yang merepresentasikan sebuah keyakinan terukur (*structured belief*).

Alur proses:
1. Menerima payload: `{ raw_text: string, source_url?: string, author_handle?: string }`.
2. Melakukan validasi input awal via skema Zod.
3. Mengirimkan prompt ekstraksi terstruktur ke OpenRouter API:
   - Identifikasi: `subject` (misal: "SOL"), `comparison_asset` (misal: "ETH"), `direction` ("OUTPERFORM" | "ABOVE_PRICE" | "BELOW_PRICE"), `target_value` (jika ada), `timeframe_days` / `deadline_iso`, `statement_summary`, `oracle_recommendation`, dan `confidence_score` (0.0 - 1.0).
4. Melakukan validasi Zod ketat pada respons JSON LLM.
5. Mengembalikan hasil ekstraksi terstruktur ke client (tanpa langsung menyimpan ke database) untuk ditinjau oleh pengguna.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengimplementasikan `omen/web/app/api/beliefs/extract/route.ts` untuk `POST /api/beliefs/extract`.
- [x] Menyediakan prompt AI terstruktur yang menghasilkan schema JSON terprediksi dan konsisten.
- [x] Melakukan validasi output LLM menggunakan Zod schema sebelum merespons ke client.
- [x] Menyediakan fallback parsing yang aman jika output LLM menyertakan markdown formatting / codeblocks.
- [x] Mengembalikan HTTP 400 untuk input tidak valid dan HTTP 502/500 jika penyedia AI mengalami kendala.
- [x] Menyusun unit test dengan mock AI client pada `omen/web/tests/api-beliefs-extract.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/extract/route.ts`
- `omen/web/lib/ai/openrouter.ts`
- `omen/web/types/belief.ts`
- `omen/web/tests/api-beliefs-extract.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Menulis unit test TDD di `omen/web/tests/api-beliefs-extract.test.ts` untuk menguji ekstraksi keyakinan relatif & absolut, pembersihan markdown fences (````json ... ````), penolakan HTTP 400 untuk payload kosong, penanganan HTTP 422 untuk schema parsing gagal, dan HTTP 502 untuk kegagalan provider.
  2. Menyusun definisi skema Zod dan TypeScript di `omen/web/types/belief.ts` (`ExtractBeliefRequestSchema`, `StructuredBeliefSchema`).
  3. Mengimplementasikan pustaka abstraksi AI client di `omen/web/lib/ai/openrouter.ts` yang berinteraksi dengan OpenRouter API secara aman.
  4. Mengimplementasikan handler endpoint serverless di `omen/web/app/api/beliefs/extract/route.ts`.
  5. Menjalankan Vitest unit testing: seluruh 6 test `api-beliefs-extract.test.ts` lulus 100%.
  6. Menjalankan pengecekan tipe `tsc --noEmit` dan linter `eslint` dengan 0 error.
- **Ringkasan File Terpengaruh:**
  - `omen/web/types/belief.ts` (Zod schemas dan tipe data request/response ekstraksi keyakinan)
  - `omen/web/lib/ai/openrouter.ts` (Abstraksi LLM client OpenRouter & parser JSON)
  - `omen/web/app/api/beliefs/extract/route.ts` (Serverless API route POST /api/beliefs/extract)
  - `omen/web/tests/api-beliefs-extract.test.ts` (Unit test suite untuk ekstraksi AI)
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Mengisolasi LLM provider abstraction pada `lib/ai/openrouter.ts` sehingga model dapat diganti atau di-switch secara modular tanpa mengubah API contract atau route logic.
  - Penegakan Zero-Comment Policy dipatuhi secara ketat pada seluruh file.
