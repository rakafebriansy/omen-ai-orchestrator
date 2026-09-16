---
id: TICKET-45
title: Integrasi Logo Resmi Omen pada Navbar, Footer, dan Shell Branding
status: Todo
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
- [ ] Logo resmi Omen (`logo.png`) terpasang secara presisi pada Navbar desktop dan drawer mobile.
- [ ] Logo resmi Omen terpasang secara konsisten pada Footer.
- [ ] Tampilan logo tajam, proporsional, dan tidak mengalami distorsi aspek rasio di Dark Mode maupun Light Mode.
- [ ] Seluruh unit test layout shell dan navbar tetap lulus 100% pada Vitest.

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
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
