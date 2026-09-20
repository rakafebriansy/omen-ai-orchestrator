---
id: TICKET-125
title: Creator Profile Auto-Registration, Live DB Backfill, and X (Twitter) Redirect
status: Done
priority: High
labels: [Backend, Database, Social, Frontend, BugFix]
---

# Deskripsi
Ketika pengguna mengajukan keyakinan (*belief submission*) baru melalui form `/create`, data belief berhasil tersimpan ke tabel `beliefs` dan pasar on-chain terbentuk. Namun, profil kreator terkait tidak otomatis terdaftar di direktori `/creators` jika kreator tersebut belum memiliki entri di tabel `creator_profiles`. Akibatnya, kreator baru tidak muncul di leaderboard direktori dan tautan redirect ke profil X (Twitter) tidak berfungsi.

Tiket ini mengimplementasikan logika *auto-registration / auto-upsert* di endpoint `POST /api/beliefs/submit` yang secara otomatis mendaftarkan profil kreator baru ke tabel `creator_profiles` dengan metadata default saat belief pertama mereka diajukan, melakukan migrasi/backfill data kreator yang sempat terlewat di database produksi, memperbaiki tautan redirect profil X (`x.com/<handle>`), serta menyusun mekanisme *graceful avatar fallback* saat layanan unavatar.io mengalami pembatasan laju (*rate limiting*).

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Endpoint `POST /api/beliefs/submit` secara otomatis memeriksa keberadaan profil di tabel `creator_profiles` berdasarkan `creator_wallet` atau `creator_handle`.
- [x] Jika belum ada, sistem melakukan *upsert/insert* profil kreator baru ke `creator_profiles` dengan data default (`display_name`, `handle`, `wallet_address`, `bio`).
- [x] Memperbaiki tautan eksternal pada kartu kreator dan profil kreator agar mengarah secara akurat ke profil media sosial X (`https://x.com/${handle.replace('@', '')}`).
- [x] Melakukan backfill terhadap kreator yang sebelumnya tidak terdaftar (`@rkfbrns`, `@rakaaaa`, `@rk98736`) di database Supabase aktif.
- [x] Menyediakan penanganan graceful degradasi avatar (gradient avatar badge dengan inisial nama) saat unavatar.io terkena 429 rate limit atau gagal dimuat.
- [x] Memastikan direktori `/creators` menampilkan semua kreator aktif beserta pasar yang mereka miliki secara real-time.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/beliefs/submit/route.ts`
- `omen/web/components/CreatorCard.tsx`
- `omen/web/app/creators/page.tsx`
- `omen/web/app/creator/[address]/page.tsx`
- `omen/web/tests/api-beliefs-submit.test.ts`

---

## AI Execution Log dan Output

- **Langkah Teknis Tereksekusi:**
  1. Memodifikasi `web/app/api/beliefs/submit/route.ts` untuk menambahkan tahap query dan upsert profil pada tabel `creator_profiles` sebelum proses pembuatan pasar on-chain.
  2. Menghubungkan wallet kreator, handle X, dan nama tampilan secara otomatis.
  3. Menjalankan query upsert data via Supabase Service Role client untuk mendaftarkan 3 akun kreator yang terlewat (`@rkfbrns`, `@rakaaaa`, `@rk98736`) dengan alamat wallet terkait.
  4. Memverifikasi redirect link di `CreatorCard.tsx` dan `CreatorProfileHeader.tsx` mengarah ke URL `https://x.com/${handle}`.
  5. Menambahkan state fallback avatar visual jika `unavatar.io/x/${handle}` mengembalikan respons non-200.

- **Ringkasan File Terpengaruh:**
  - `omen/web/app/api/beliefs/submit/route.ts`
  - `omen/web/components/CreatorCard.tsx`
  - `omen/web/app/creators/page.tsx`

- **Catatan dan Keputusan Arsitektural:**
  - Relasi dua arah antara `beliefs` dan `creator_profiles` kini terikat secara otomatis pada siklus hidup submission, menghilangkan disparitas data antara pasar keyakinan dan direktori sosial.
