# Design System — Omen

## 1. Identitas Merek (*Brand Identity*)

**Omen** mengusung konsep visual **OpenZeppelin Institutional Web3 / Developer-First Aesthetic** terinspirasi langsung dari standar desain [OpenZeppelin](https://www.openzeppelin.com) dan [OpenZeppelin Contracts](https://www.openzeppelin.com/solidity-contracts). Pendekatan desain ini mengutamakan keterbacaan tingkat tinggi (*high legibility*), kredibilitas institusional, struktur grid yang rapi dan presisi, kontras warna tajam, gradasi atmosferik halus (*subtle atmospheric gradients*), serta elemen kartu berbasis *clean white surface* dan *slate/navy accents*.

* **Vibe:** Institutional, High-Trust, Clean, Precision-Engineered, Developer-First, Crisp.
* **Tone:** Kredibel, Transparan, Andal, Objektif.

---

## 2. Palet Warna dan Token (*Color Palette and Tokens*)

### 2.1 Color Tokens dan Tailwind Configuration
| Token Name | Hex Code | Deskripsi dan Penggunaan Utama |
|---|---|---|
| `primary-blue` | `#4E5EE4` | Warna primer utama jenama Omen (OpenZeppelin Royal Cobalt), tombol CTA utama, link aktif. |
| `primary-blue-hover` | `#3D4CC8` | Status hover tombol primer dan highlight navigasi. |
| `primary-blue-soft` | `#EEF2FF` | Latar belakang badge biru ringan, chip aktif, container highlight. |
| `accent-navy` | `#0F172A` | Teks heading utama (*Slate-900*), header bar, footer, dan panel kode gelap. |
| `yes-green` | `#10B981` | Tombol dan pool taruhan **YES**, status pasar untung, status quest selesai (*Claimed*). |
| `yes-green-soft` | `#ECFDF5` | Latar belakang pool Yes, badge status aman (*Emerald-50*). |
| `no-red` | `#F43F5E` | Tombol dan pool taruhan **NO**, status pasar rugi/gagal, peringatan penutupan (*Rose-500*). |
| `no-red-soft` | `#FFF1F2` | Latar belakang pool No (*Rose-50*). |
| `warning-amber` | `#F59E0B` | Status pasar akan segera ditutup (*Closing Soon*), status streak. |
| `warning-soft` | `#FEF3C7` | Latar belakang badge peringatan (*Amber-50*). |
| `bg-main` | `#FFFFFF` | Latar belakang kanvas utama (*Clean White*). |
| `bg-subtle` | `#F8FAFC` | Latar belakang seksi sekunder (*Slate-50*). |
| `card-surface` | `#FFFFFF` | Permukaan kartu (*Card Surface*) dengan border crisp. |
| `border-subtle` | `#E2E8F0` | Garis pembatas kartu dan tabel (*Slate-200*). |
| `text-primary` | `#0F172A` | Teks heading dan isi utama (*Slate-900*). |
| `text-muted` | `#64748B` | Teks sekunder, label tabel, deskripsi misi (*Slate-500*). |

---

### 2.2 Sistem Gradasi (*Gradient System — OpenZeppelin Institutional*)

Mengadopsi spesifikasi gradasi otentik OpenZeppelin untuk menciptakan kedalaman visual (*visual depth*), hierarki display yang memukau, dan pencahayaan atmosferik (*ambient atmosphere*):

#### 1. Tipografi dan Teks Bergradasi (*Text Gradients*)
* **Cobalt to Electric Blue Display (`gradient-text-blue`):**
  * **Formula CSS:** `linear-gradient(91.08deg, #0A74F2 35.42%, #4E5EE4 64.41%)`
  * **Tailwind Utility:** `bg-gradient-to-r from-[#0A74F2] to-[#4E5EE4] bg-clip-text text-transparent`
  * **Penggunaan:** Kata kunci headline H1 pada Hero Section, angka nominal Total Value Locked (TVL), dan highlight judul fitur utama.
* **Soft Indigo to Lavender Display (`gradient-text-light`):**
  * **Formula CSS:** `linear-gradient(91.08deg, #717DE8 35.42%, #C5CAF7 64.41%)`
  * **Tailwind Utility:** `bg-gradient-to-r from-[#717DE8] to-[#C5CAF7] bg-clip-text text-transparent`
  * **Penggunaan:** Teks heading pada panel berlatar gelap (Navy header / Dark code preview / Footer CTA).
* **Vertical Sub-accent Gradient:**
  * **Formula CSS:** `linear-gradient(174.73deg, #717DE8 19.9%, #C5CAF7 83.98%)`
  * **Penggunaan:** Badge aksen vertikal dan pill tag kategori eksklusif.

#### 2. Tombol Berlapis dan Interaktif (*Layered Button Gradients*)
* **Institutional Royal Cobalt Button (`btn-gradient-primary`):**
  * **Formula CSS:**
    ```css
    background:
      linear-gradient(180deg, #4F5EE5 0%, #4553D2 100%) padding-box,
      linear-gradient(180deg, #7985F2 0%, #313C9E 100%) border-box;
    border: 1px solid transparent;
    box-shadow: 0px 1px 2px rgba(15, 23, 42, 0.08), 0px 0px 12px rgba(78, 94, 228, 0.20);
    ```
  * **Efek Hover:** Elevasi shadow `box-shadow: 0px 0px 20px rgba(78, 94, 228, 0.35); filter: brightness(1.03);`
  * **Penggunaan:** Tombol aksi primer seperti "Connect Wallet", "Explore Markets", dan "Confirm Prediction".
* **Subtle Slate Pill Button (`btn-gradient-subtle`):**
  * **Formula CSS:**
    ```css
    background:
      linear-gradient(180deg, #F6F6F9 0%, #DCE1E8 100%) padding-box,
      linear-gradient(180deg, #CDCDF3 0%, #BDC1CB 100%) border-box;
    border: 1px solid transparent;
    ```
  * **Penggunaan:** Tombol sekunder ("Earn Quest Points", "Documentation", filter kategori non-aktif).

#### 3. Latar Belakang dan Atmosfer Kanvas (*Canvas Atmosphere Gradients*)
* **Hero Atmosphere Fade (`bg-hero-atmosphere`):**
  * **Formula CSS:** `linear-gradient(180deg, #FFFFFF 33%, #E7F3FC 80%, #F6F6F9 100%)`
  * **Penggunaan:** Latar kanvas Hero Section yang memberikan transisi alami dari putih bersih ke rona biru langit lembut dan mendarat pada warna latar seksi berikutnya.
* **Section Transition Gradient (`bg-section-subtle`):**
  * **Formula CSS:** `linear-gradient(180deg, #FCFCFD 0%, #F6F6F9 100%)`
  * **Penggunaan:** Transisi antar seksi beranda dan dashboard untuk memisahkan konten tanpa garis kaku.
* **Ambient Radial Mesh Glow (`bg-radial-glow`):**
  * **Formula CSS:** `radial-gradient(ellipse 80% 50% at 50% -20%, rgba(78, 94, 228, 0.08) 0%, rgba(255, 255, 255, 0) 100%)`
  * **Penggunaan:** Efek pendaran lembut di balik navbar dan hero banner untuk memberikan kesan modernitas Web3 tanpa menurunkan rasio kontras teks.

#### 4. Border Kartu dan Conic Shimmer (*Card Border and Conic Accents*)
* **Conic Accent Glow (`conic-card-glow`):**
  * **Formula CSS:** `conic-gradient(transparent 0deg, transparent 180deg, rgba(78, 94, 228, 0.4) 360deg)`
  * **Penggunaan:** Border animasi rotasi halus untuk kartu pasar prediksi berstatus unggulan (*Featured / Trending Markets*).
* **Subtle Card Top-Edge Gradient:**
  * **Formula CSS:** `linear-gradient(180deg, rgba(226, 232, 240, 0.9) 0%, rgba(241, 245, 249, 0.4) 100%)`
  * **Penggunaan:** Border halus kartu metrik statistik dan daftar misi.

---

## 3. Tipografi (*Typography*)

### 3.1 Font Families
* **Primary Sans Font:** `Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif` — Digunakan untuk seluruh teks judul, paragraf, tombol, dan label navigasi.
* **Monospace Numeric dan Code Font:** `"JetBrains Mono", "SF Mono", Menlo, Consolas, monospace` — Digunakan khusus untuk alamat dompet (*0x...*), nilai pool taruhan, rasio odds/persentase, saldo poin, dan kode cuplikan smart contract.

### 3.2 Skala Tipografi
| Tingkat | Ukuran (Tailwind) | Ketebalan (*Weight*) | Penggunaan |
|---|---|---|---|
| **Display H1** | `text-4xl` s/d `text-5xl` (`36px` - `48px`) | `font-extrabold` (800) | Judul utama landing page dan hero banner |
| **Heading 2 (H2)** | `text-2xl` s/d `text-3xl` (`24px` - `30px`) | `font-bold` (700) | Judul seksi dashboard (Predictions, Quests, Leaderboard) |
| **Heading 3 (H3)** | `text-lg` s/d `text-xl` (`18px` - `20px`) | `font-semibold` (600) | Judul kartu pasar prediksi dan kartu misi |
| **Body Regular** | `text-sm` s/d `text-base` (`14px` - `16px`) | `font-normal` (400) / `500` | Deskripsi pasar, detail tugas, teks paragraf |
| **Caption / Odds** | `text-xs` (`12px`) | `font-mono font-medium` | Label waktu penutupan, rasio pool, alamat wallet singkat |

---

## 4. Sistem Spacing, Tata Letak, dan Breakpoints

* **Canvas Max Width:** `max-w-7xl` (`1280px`) untuk dashboard terpusat.
* **Grid Spacing:** Mengikuti standar Tailwind (`gap-4`, `gap-6`, `gap-8`, `p-6`).
* **Border dan Shadows:**
  * Container / Cards: `rounded-xl` (`12px`) / `rounded-2xl` (`16px`), `border border-slate-200`, `shadow-sm hover:shadow-md transition-shadow`.
  * Buttons / Input Fields: `rounded-lg` (`8px`), font-weight `600`.
  * Badges / Pill Tags: `rounded-full` (`9999px`), padding `py-1 px-3`, font-weight `600`.
* **Responsive Breakpoints:**
  * `sm` (`640px`): Tata letak mobile 1 kolom.
  * `md` (`768px`): 2 kolom kartu prediksi, tab navigasi horizontal.
  * `lg` (`1024px`): 3 kolom kartu prediksi, tampilan leaderboard penuh.
  * `xl` (`1280px`): Tata letak desktop optimal dengan panel ringkasan samping.

---

## 5. Library Komponen UI (*UI Components*)

### 5.1 Kartu Pasar Prediksi (*Prediction Market Card*)
* Wadah: `bg-white border border-slate-200 rounded-xl p-6 shadow-sm hover:shadow-md transition-all hover:border-slate-300`.
* Bilah Progres Pool (*Pool Ratio Bar*): Dual progress bar dengan warna `bg-emerald-500` (Yes) dan `bg-rose-500` (No) dengan label persentase odds yang tajam.
* Tombol Aksi: Tombol Yes (`bg-emerald-50 text-emerald-700 border border-emerald-200 hover:bg-emerald-100`) dan No (`bg-rose-50 text-rose-700 border border-rose-200 hover:bg-rose-100`).

### 5.2 Widget Daily Check-in dan Streak
* Kartu dengan border `border-slate-200`, latar belakang `bg-slate-50`, indikator streak warna amber/emas, dan tombol `btn-primary` (`bg-[#4E5EE4] text-white hover:bg-[#3D4CC8]`).

### 5.3 Baris Misi Quest (*Quest Row Item*)
* Kartu horizontal putih dengan border `border-slate-200`, badge reward poin biru (`bg-indigo-50 text-indigo-700 border border-indigo-200`), dan tombol aksi.

### 5.4 Modal Pemasangan Taruhan (*Betting Modal*)
* Modal putih bersih dengan backdrop blur, slider input nominal ETH, estimasi return proporsional, dan tombol submit `bg-[#4E5EE4]`.

### 5.5 Tabel Peringkat (*Leaderboard Table*)
* Tabel data terstruktur dengan header `bg-slate-50 text-slate-500 uppercase text-xs`, baris bergaris `border-b border-slate-100 hover:bg-slate-50/80`, dan badge rank 1-3.

---

## 6. Standar Aksesibilitas (a11y) dan Animasi

1. **WCAG 2.1 AA Compliance:** Seluruh teks di atas latar putih dan badge memenuhi rasio kontras 4.5:1 (misal teks `#0F172A` di atas `#FFFFFF` menghasilkan kontras 15:1).
2. **ARIA Screen Reader Labels:**
   * Tombol taruhan memiliki atribut `aria-label="Bet on Yes for [Market Title]"`.
   * Streak counter memiliki label deskriptif `aria-label="Current check-in streak: X days"`.
   * Saldo poin pengguna memuat `aria-live="polite"` untuk pengumuman instan saat klaim berhasil.
3. **Reduced Motion:** Animasi transisi halus dan hover lift menghormati preferensi `@media (prefers-reduced-motion: reduce)`.

---

## 7. Validasi Purwarupa (Prototyping)

Setiap rancangan komponen visual baru sebelum diimplementasikan ke Next.js dapat divalidasi terlebih dahulu dalam format berkas tunggal HTML di dalam direktori `nodes/omen/prototypes/`.
