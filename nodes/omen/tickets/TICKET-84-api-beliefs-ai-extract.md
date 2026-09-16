---
id: TICKET-84
title: Pembuatan API Route Ekstraksi AI Terstruktur (POST /api/beliefs/extract)
status: Todo
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
- [ ] Mengimplementasikan `omen/web/app/api/beliefs/extract/route.ts` untuk `POST /api/beliefs/extract`.
- [ ] Menyediakan prompt AI terstruktur yang menghasilkan schema JSON terprediksi dan konsisten.
- [ ] Melakukan validasi output LLM menggunakan Zod schema sebelum merespons ke client.
- [ ] Menyediakan fallback parsing yang aman jika output LLM menyertakan markdown formatting / codeblocks.
- [ ] Mengembalikan HTTP 400 untuk input tidak valid dan HTTP 502/500 jika penyedia AI mengalami kendala.
- [ ] Menyusun unit test dengan mock AI client pada `omen/web/tests/api-beliefs-extract.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/extract/route.ts`
- `omen/web/lib/ai/openrouter.ts`
- `omen/web/types/belief.ts`
- `omen/web/tests/api-beliefs-extract.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
