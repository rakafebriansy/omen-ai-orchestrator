---
id: TICKET-113
title: Fix Creators Directory Supabase Integration and Harmonize API Payload Contracts
status: Done
priority: High
labels: [Frontend, Backend, Supabase, Integration, Bug]
---

# Deskripsi
Halaman direktori kreator (`/creators` / `web/app/creators/page.tsx`) saat ini belum merender data dinamis dari Supabase secara sempurna di *live deployment* (https://omen-iota.vercel.app/creators). 

### Akar Masalah:
1. **Payload Contract Mismatch:**
   - Endpoint `web/app/api/creators/route.ts` mengembalikan response berformat `{ success: true, data: formattedProfiles }`.
   - Komponen `web/app/creators/page.tsx` mengecek `data.creators` (`if (data.creators)`), sehingga gagal membaca array data dan otomatis jatuh ke *fallback state* statis `INITIAL_CREATORS` (Vitalik Buterin & Satoshi Disciple).
2. **Ketiadaan Dynamic Aggregation pada Creator Baru:**
   - Saat pengguna membuat *Social Belief* baru di `/create`, data tersimpan di tabel `beliefs` dengan kolom `author` / `creator_address`.
   - Jika tabel `creator_profiles` belum di-seed secara manual di Supabase, endpoint `GET /api/creators` mengembalikan array kosong `[]`. Diperlukan agregasi otomatis dari tabel `beliefs` agar setiap kreator baru yang aktif otomatis terdaftar di direktori `/creators`.
3. **Penyelarasan Halaman Profil Creator (`/creator/[address]`):**
   - Endpoint `GET /api/creators/[address]/route.ts` dan halaman `web/app/creator/[address]/page.tsx` perlu diselaraskan agar dapat mencari berdasarkan `wallet_address` (contoh: `0x123...`) maupun `@handle` (contoh: `@vitalik.eth`), serta menarik riwayat pasar belief terkait langsung dari database.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Harmonisasi response `GET /api/creators` agar mengembalikan `{ success: true, data: formattedProfiles, creators: formattedProfiles, total, limit, offset }`.
- [x] Implementasikan mekanisme *dynamic aggregation fallback* pada `GET /api/creators`: jika tabel `creator_profiles` kosong, lakukan agregasi profil dari tabel `beliefs` (menghitung total belief, belief terkonfirmasi EIP-712, dan estimasi akurasi/volume).
- [x] Perbarui `web/app/creators/page.tsx` agar memproses `data.data || data.creators` secara andal, menampilkan *skeleton loading* saat memuat, dan menyajikan *empty state* yang informatif jika belum ada kreator.
- [x] Harmonisasi `GET /api/creators/[address]/route.ts` dan `web/app/creator/[address]/page.tsx` agar mendukung pencarian fleksibel via address maupun handle, serta menampilkan daftar *beliefs* aktif dan teresolusi dari kreator bersangkutan.
- [x] Tulis dan perbarui unit test Vitest pada `web/tests/api-creators.test.ts` dan komponen terkait untuk memastikan data Supabase terhubung 100%.
- [x] Pastikan seluruh kode mematuhi Zero-Comment Policy, lulus `npx tsc --noEmit`, dan 0 error ESLint.

## Target Lingkup File (Affected Files)
- `web/app/api/creators/route.ts`
- `web/app/api/creators/[address]/route.ts`
- `web/app/creators/page.tsx`
- `web/app/creator/[address]/page.tsx`
- `web/tests/api-creators.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Menyelaraskan struktur respons `GET /api/creators` mengembalikan `{ success: true, data: formattedProfiles, creators: formattedProfiles, total, limit, offset }` untuk kompatibilitas ganda (dual-contract payload).
  2. Menambahkan fallback dynamic aggregation dari tabel `beliefs` pada `GET /api/creators` dan `GET /api/creators/[address]`, mengelompokkan riwayat belief per author/kreator secara real-time saat tabel `creator_profiles` belum di-seed.
  3. Memperbarui `web/app/creators/page.tsx` untuk membaca `data.data || data.creators` dengan skeleton loader dan empty state.
  4. Memperbarui `web/app/creator/[address]/page.tsx` untuk mengekstrak profil kreator dan array beliefs yang tersinkronisasi.
  5. Menyelaraskan unit test `web/tests/api-creators.test.ts` untuk memvalidasi pencarian, akurasi, dan error fallback.
  6. Memverifikasi seluruh pengujian dengan Zero-Comment Policy, `npx tsc --noEmit`, dan `npm run lint`.
- **Ringkasan File Terpengaruh:**
  - `web/app/api/creators/route.ts`
  - `web/app/api/creators/[address]/route.ts`
  - `web/app/creators/page.tsx`
  - `web/app/creator/[address]/page.tsx`
  - `web/tests/api-creators.test.ts`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menerapkan arsitektur dual-source: membaca tabel `creator_profiles` utama dan fallback agregasi cerdas dari tabel `beliefs` untuk menjamin kreator baru selalu tampil seketika tanpa batch manual.
