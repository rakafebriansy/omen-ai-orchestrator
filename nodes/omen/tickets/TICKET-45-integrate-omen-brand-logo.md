---
id: TICKET-45
title: Integrasi Logo Resmi Omen pada Navbar, Footer, dan Shell Branding
status: Done
priority: Medium
labels: [Frontend, UI, Branding]
---

# Deskripsi
Mengintegrasikan aset visual logo resmi Omen (`web/public/images/logo.png`) ke seluruh titik sentral antarmuka web, menggantikan placeholder simbol "Ω" pada komponen header navigasi `Navbar.tsx`, footer aplikasi `Footer.tsx`, serta metadata layout aplikasi.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Integrasi Logo (`logo.png`)
1. **Header Navigasi (`Navbar.tsx`):**
   - Menggantikan placeholder simbol kotak "Ω" dengan komponen Next.js `<Image src="/images/logo.png" alt="Omen Logo" width={32} height={32} />`.
   - Menjaga rasio aspek tetap proporsional dan tajam di Dark Mode maupun Light Mode tanpa pergeseran tata letak (*zero layout shift*).
2. **Footer Shell (`Footer.tsx`):**
   - Menyelaraskan brand mark di footer dengan logo resmi Omen bersanding dengan teks "OMEN".
3. **Favicon & Metadata (`app/layout.tsx`):**
   - Memastikan tautan ikon aplikasi merujuk pada logo resmi Omen.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Logo resmi Omen (`logo.png`) terpasang secara presisi pada Navbar desktop dan drawer mobile.
- [x] Logo resmi Omen terpasang secara konsisten pada Footer.
- [x] Tampilan logo tajam, proporsional, dan tidak mengalami distorsi aspek rasio di Dark Mode maupun Light Mode.
- [x] Seluruh unit test layout shell dan navbar tetap lulus 100% pada Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/Navbar.tsx`
- `omen/web/components/Footer.tsx`
- `omen/web/app/layout.tsx`
- `omen/web/tests/navbar.test.tsx`
- `omen/web/tests/footer.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Memodifikasi `Navbar.tsx` untuk mengimpor dan merender `<Image src="/images/logo.png" alt="Omen Logo" width={32} height={32} className="w-8 h-8 object-contain" priority />` pada desktop header brand mark.
  2. Memodifikasi `Footer.tsx` untuk merender `<Image src="/images/logo.png" alt="Omen Logo" width={28} height={28} className="w-7 h-7 object-contain" />` bersanding dengan teks OMEN.
  3. Menambahkan ikon favicon resmi Omen pada objek metadata di `app/layout.tsx`.
  4. Memperbarui test suite `navbar.test.tsx` dan `footer.test.tsx` untuk memvalidasi atribut alt image logo resmi Omen.
  5. Memverifikasi seluruh pengujian Vitest (total 65/65 tests pass 100%), type check TypeScript bersih, dan Zero-Comment Policy terjaga mutlak.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/Navbar.tsx` [Modified]
  - `omen/web/components/Footer.tsx` [Modified]
  - `omen/web/app/layout.tsx` [Modified]
  - `omen/web/tests/navbar.test.tsx` [Modified]
  - `omen/web/tests/footer.test.tsx` [Modified]
  - `nodes/omen/tickets/TICKET-45-integrate-omen-brand-logo.md` [Updated]
  - `nodes/omen/CHANGELOG.md` [Updated]
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggunakan Next.js Image Optimization dengan prop `priority` pada Navbar brand mark untuk memaksimalkan First Contentful Paint (FCP) dan mencegah Cumulative Layout Shift (CLS).
