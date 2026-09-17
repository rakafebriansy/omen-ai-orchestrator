---
id: TICKET-111
title: Live AI Review Integration and Free AI API Key Setup
status: Todo
priority: High
labels: [Backend, AI, Integration, Feature]
---

# Deskripsi
Saat ini endpoint ekstraksi parameter opini sosial (`web/app/api/beliefs/extract/route.ts`) masih menggunakan ekstraksi heuristik/mock. Tiket ini bertujuan untuk mengintegrasikan model LLM riil menggunakan penyedia API AI gratis (free tier) guna melakukan parsing opini teks alami menjadi parameter pasar prediksi terstruktur secara akurat.

### Rekomendasi Penyedia Free AI API Key:
1. **OpenRouter (Free Tier Models)**:
   - Endpoint: `https://openrouter.ai/api/v1/chat/completions`
   - Model Gratis: `meta-llama/llama-3.3-70b-instruct:free`, `google/gemini-2.0-flash-exp:free`, `mistralai/mistral-7b-instruct:free`
   - Cara Mendapatkan: Daftar di [openrouter.ai](https://openrouter.ai/), buat API key gratis dengan rate limit harian yang ramah untuk development.
2. **Groq Cloud (Free Tier Fast Inference)**:
   - Endpoint: `https://api.groq.com/openai/v1/chat/completions`
   - Model Gratis: `llama-3.3-70b-versatile`, `llama-3.1-8b-instant`, `mixtral-8x7b-32768`
   - Cara Mendapatkan: Daftar di [console.groq.com](https://console.groq.com/) dan buat API key tanpa biaya.
3. **Google AI Studio (Gemini 1.5 Flash / 2.0 Flash)**:
   - Endpoint: `https://generativelanguage.googleapis.com/v1beta`
   - Model Gratis: `gemini-1.5-flash`, `gemini-2.0-flash`
   - Cara Mendapatkan: Dapatkan Google AI API Key gratis di [aistudio.google.com](https://aistudio.google.com/).

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Implementasikan LLM adapter multi-provider pada `web/app/api/beliefs/extract/route.ts` atau `web/lib/ai/` yang mendukung OpenRouter, Groq, dan Gemini.
- [ ] Buat prompt sistem terstruktur yang mewajibkan LLM merespons dalam format JSON murni dengan skema:
  - `statement`: string kalimat deklaratif pasar prediksi
  - `subject`: string aset/entitas (contoh: BTC, ETH, AI, MACRO)
  - `direction`: "ABOVE" | "BELOW" | "YES" | "NO"
  - `target_price`: number (jika ada threshold harga)
  - `target_time`: string tanggal ISO (YYYY-MM-DD)
  - `category`: string ("Crypto" | "AI" | "Macro" | "Tech")
  - `confidence_score`: number (0-100)
- [ ] Sertakan mekanisme fallback otomatis ke heuristik lokal berkecepatan tinggi jika `OPENROUTER_API_KEY`, `GROQ_API_KEY`, atau `GEMINI_API_KEY` belum disetel atau mengalami *rate limit*.
- [ ] Perbarui `.env.example` dengan variabel lingkungan opsional:
  - `OPENROUTER_API_KEY=`
  - `GROQ_API_KEY=`
  - `GEMINI_API_KEY=`
- [ ] Tulis unit test komprehensif menggunakan Vitest untuk memvalidasi parser output LLM dan skenario kegagalan/fallback.

## Target Lingkup File (Affected Files)
- `web/app/api/beliefs/extract/route.ts`
- `web/lib/ai/extractor.ts`
- `web/.env.example`
- `web/tests/api-beliefs-extract.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Tiket diinisialisasi untuk implementasi integrasi AI riil.
- **Ringkasan File Terpengaruh:**
  - `nodes/omen/tickets/TICKET-111-live-ai-review-integration-and-free-api-key-setup.md`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan arsitektur universal adapter berstandar OpenAI Chat Completions schema agar mudah dihubungkan dengan OpenRouter maupun Groq.
