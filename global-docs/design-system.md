# Design System — Omen

## 1. Identitas Merek (*Brand Identity*)

**Omen** mengusung konsep visual **OpenZeppelin Institutional Web3 / Developer-First Aesthetic** terinspirasi langsung dari [OpenZeppelin Contracts](https://www.openzeppelin.com/solidity-contracts?ref=landingfolio). Pendekatan desain ini mengutamakan keterbacaan tingkat tinggi (*high legibility*), kredibilitas institusional, struktur grid yang rapi dan presisi, kontras warna tajam, serta elemen kartu berbasis *clean white surface* dan *slate/navy accents*.

* **Vibe:** Institutional, High-Trust, Clean, Precision-Engineered, Developer-First, Crisp.
* **Tone:** Kredibel, Transparan, Andal, Objektif.

---

## 2. Palet Warna (*Color Palette*)

### 2.1 Color Tokens & Tailwind Configuration
| Token Name | Hex Code | Deskripsi & Penggunaan Utama |
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

## 3. Tipografi (*Typography*)

### 3.1 Font Families
* **Primary Sans Font:** `Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif` — Digunakan untuk seluruh teks judul, paragraf, tombol, dan label navigasi.
* **Monospace Numeric & Code Font:** `"JetBrains Mono", "SF Mono", Menlo, Consolas, monospace` — Digunakan khusus untuk alamat dompet (*0x...*), nilai pool taruhan, rasio odds/persentase, saldo poin, dan kode cuplikan smart contract.

### 3.2 Skala Tipografi
| Tingkat | Ukuran (Tailwind) | Ketebalan (*Weight*) | Penggunaan |
|---|---|---|---|
| **Display H1** | `text-4xl` s/d `text-5xl` (`36px` - `48px`) | `font-extrabold` (800) | Judul utama landing page & hero banner |
| **Heading 2 (H2)** | `text-2xl` s/d `text-3xl` (`24px` - `30px`) | `font-bold` (700) | Judul seksi dashboard (Predictions, Quests, Leaderboard) |
| **Heading 3 (H3)** | `text-lg` s/d `text-xl` (`18px` - `20px`) | `font-semibold` (600) | Judul kartu pasar prediksi & kartu misi |
| **Body Regular** | `text-sm` s/d `text-base` (`14px` - `16px`) | `font-normal` (400) / `500` | Deskripsi pasar, detail tugas, teks paragraf |
| **Caption / Odds** | `text-xs` (`12px`) | `font-mono font-medium` | Label waktu penutupan, rasio pool, alamat wallet singkat |

---

## 4. Sistem Spacing, Tata Letak, & Breakpoints

* **Canvas Max Width:** `max-w-7xl` (`1280px`) untuk dashboard terpusat.
* **Grid Spacing:** Mengikuti standar Tailwind (`gap-4`, `gap-6`, `gap-8`, `p-6`).
* **Border & Shadows:**
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

### 5.2 Widget Daily Check-in & Streak
* Kartu dengan border `border-slate-200`, latar belakang `bg-slate-50`, indikator streak warna amber/emas, dan tombol `btn-primary` (`bg-[#4E5EE4] text-white hover:bg-[#3D4CC8]`).

### 5.3 Baris Misi Quest (*Quest Row Item*)
* Kartu horizontal putih dengan border `border-slate-200`, badge reward poin biru (`bg-indigo-50 text-indigo-700 border border-indigo-200`), dan tombol aksi.

### 5.4 Modal Pemasangan Taruhan (*Betting Modal*)
* Modal putih bersih dengan backdrop blur, slider input nominal ETH, estimasi return proporsional, dan tombol submit `bg-[#4E5EE4]`.

### 5.5 Tabel Peringkat (*Leaderboard Table*)
* Tabel data terstruktur dengan header `bg-slate-50 text-slate-500 uppercase text-xs`, baris bergaris `border-b border-slate-100 hover:bg-slate-50/80`, dan badge rank 1-3.

---

## 6. Standar Aksesibilitas (a11y) & Animasi

1. **WCAG 2.1 AA Compliance:** Seluruh teks di atas latar putih dan badge memenuhi rasio kontras 4.5:1 (misal teks `#0F172A` di atas `#FFFFFF` menghasilkan kontras 15:1).
2. **ARIA Screen Reader Labels:**
   * Tombol taruhan memiliki atribut `aria-label="Bet on Yes for [Market Title]"`.
   * Streak counter memiliki label deskriptif `aria-label="Current check-in streak: X days"`.
   * Saldo poin pengguna memuat `aria-live="polite"` untuk pengumuman instan saat klaim berhasil.
3. **Reduced Motion:** Animasi transisi halus dan hover lift menghormati preferensi `@media (prefers-reduced-motion: reduce)`.

---

## 7. Validasi Purwarupa (Prototyping)

Setiap rancangan komponen visual baru sebelum diimplementasikan ke Next.js dapat divalidasi terlebih dahulu dalam format berkas tunggal HTML di dalam direktori `nodes/omen/prototypes/`.
