---
id: TICKET-50
title: Integrasi Real Data & API Mutation pada Halaman Quests & Daily Check-in
status: Done
priority: High
labels: [Frontend, Backend, Gamification, Quests, Integration]
---

# Deskripsi
Halaman `app/quests/page.tsx` dan komponen `DailyCheckinWidget.tsx` saat ini menggunakan array statis `INITIAL_QUESTS` dan in-memory state. Tiket ini bertugas menghubungkan daftar quest ke endpoint `GET /api/quests?wallet_address=...`, menghubungkan tombol verifikasi misi ke `POST /api/quests/[id]/complete`, serta menghubungkan klaim streak ke `POST /api/checkin`.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] `app/quests/page.tsx` memanggil `GET /api/quests` dengan menyertakan wallet pengguna aktif untuk menentukan status `is_completed`.
- [x] Tombol aksi/verifikasi pada `QuestCard` memanggil `POST /api/quests/[id]/complete` dengan payload `{ wallet_address }` dan memperbarui saldo total poin seketika.
- [x] `DailyCheckinWidget.tsx` memuat data `streak_count` dan `last_checkin_at` riil pengguna dari database Supabase.
- [x] Tombol klaim daily check-in memanggil `POST /api/checkin` dengan payload `{ wallet_address }`, memperbarui cooldown timer 24 jam dan mengkalkulasi multiplier streak secara akurat.
- [x] Menampilkan toast notifikasi perolehan poin sukses.

## Target Lingkup File (Affected Files & TODO Locations)
- [quests/page.tsx:L1](../../../../omen/web/app/quests/page.tsx#L1)
- [DailyCheckinWidget.tsx:L1](../../../../omen/web/components/DailyCheckinWidget.tsx#L1)
- [checkin-widget.test.tsx:L1](../../../../omen/web/tests/checkin-widget.test.tsx#L1)
- [quest-card.test.tsx:L1](../../../../omen/web/tests/quest-card.test.tsx#L1)

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menghubungkan `app/quests/page.tsx` ke endpoint `GET /api/quests?wallet_address=...` untuk fetching real-time data misi gamifikasi dari basis data Supabase.
  2. Mengintegrasikan mutasi `POST /api/quests/[id]/complete` pada aksi verifikasi tugas untuk menambahkan reward poin dan mencatat riwayat ke tabel `points_events`.
  3. Mengintegrasikan `DailyCheckinWidget.tsx` dengan `POST /api/checkin` untuk mutasi streak harian dan proteksi cooldown timer 24 jam.
  4. Seluruh 7 unit tests di `checkin-widget.test.tsx` dan `quest-card.test.tsx` lulus 100% dan mematuhi Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `omen/web/app/quests/page.tsx`, `omen/web/components/DailyCheckinWidget.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan optimistic update pada state total poin untuk responsivitas visual instan sebelum request Supabase selesai.
