---
id: TICKET-96
title: Implementasi Market Resolution Engine Berbasis Data Oracle Otomatis
status: Todo
priority: High
labels: [Backend, Oracle, Resolution, Engine]
---

# Deskripsi
Tiket ini membangun mesin penyelesaian pasar otomatis (*Market Resolution Engine*) di sisi server untuk menutup dan menyelesaikan pasar keyakinan yang telah melewati masa berlakunya (*deadline expiration*).

Alur kerja engine:
1. Menemukan seluruh pasar dengan status `OPEN` yang telah melewati `close_time` (`now >= close_time`).
2. Mengubah status pasar menjadi `CLOSED` (menghentikan penerimaan setoran posisi baru).
3. Mengambil snapshot harga akhir (*END snapshot*) dari Chainlink Oracle feed via `POST /api/oracle/snapshot`.
4. Mengevaluasi kriteria resolusi menggunakan modul `chainlink.ts` untuk menentukan pemenang (`AGREE_WON`, `DISAGREE_WON`, atau `VOID`).
5. Memanggil fungsi on-chain `OmenMarket.resolveMarket(outcome)` menggunakan admin resolver private key.
6. Memperbarui database Supabase via `POST /api/markets/[id]/resolve`.
7. Menyediakan fail-safe fallback: Jika oracle mengalami downtime atau malfungsi data feed, pasar ditandai sebagai `VOID` agar seluruh partisipan dapat melakukan penarikan refund penuh 100%.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan `omen/web/lib/market/resolution-engine.ts`.
- [ ] Menyediakan fungsi `processPendingResolutions()` yang dapat dipicu oleh cron job scheduler atau webhook.
- [ ] Menangani eksekusi on-chain `resolveMarket` dengan manajemen gas fee dan konfirmasi receipt.
- [ ] Mengimplementasikan fail-safe fallback `voidMarket` jika data oracle tidak tersedia atau terjadi anomali harga ekstrem.
- [ ] Menyusun unit test pada `omen/web/tests/resolution-engine.test.ts` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/lib/market/resolution-engine.ts`
- `omen/web/tests/resolution-engine.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
