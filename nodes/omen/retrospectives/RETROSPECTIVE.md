# AI Agent Retrospective Log — Omen

Dokumen ini merekam secara kronologis setiap kesalahan teknis, halusinasi konseptual, atau rintangan berat yang dihadapi AI Agent. Log ini digunakan untuk pembelajaran berkelanjutan.

**Format Pencatatan:** AI Agent wajib menaruh catatan terbaru di posisi paling atas (*reverse-chronological*).

---

## [2026-09-16] — Retrospective: Anti-Slop Design & Icon, Layout Shift, dan Gaya Badge UI

### Konteks Sesi
Sesi TICKET-04 (Landing Overview Page) melibatkan serangkaian iterasi intensif perbaikan visual pada komponen landing page Omen. Selama sesi ini, developer mengoreksi AI Agent atas beberapa pola desain "slop" (konten generik, miskin konteks, dan tidak sesuai standar) yang terus berulang.

---

### Pola Slop #1: Penggunaan Emoji sebagai Ikon Kategori/Tab

**Kesalahan:** AI Agent menggunakan emoji teks biasa (🔥, 📈, ₿, dll.) sebagai ikon pada tab filter kategori di komponen `TrendingMarketsTeaser.tsx`.

**Dampak:** Tampilan terlihat seperti aplikasi konsumen biasa, bukan platform DeFi/Web3 institusional. Emoji tidak dapat diatur ukurannya secara presisi, inkonsisten antar OS (rendering berbeda di Windows/Mac/Linux), dan terasa tidak profesional.

**Solusi yang Diterapkan:**
- Mengunduh aset ikon PNG resmi dari sumber otentik (CoinGecko/Cryptologos) untuk Bitcoin, Ethereum, Arbitrum, flame/hot, dan globe/macro.
- Mengonversi seluruh ikon ke format **WebP** dengan kompresi optimal (`cwebp -q 95 -alpha_q 100`) untuk mempertahankan transparansi dan bobot ringan.
- Mengintegrasikan seluruh ikon via komponen `next/image` dengan atribut `priority` untuk preloading.

**Aturan untuk AI Agent berikutnya:** DILARANG menggunakan emoji sebagai ikon UI fungsional. Gunakan selalu aset SVG/WebP/PNG resmi yang diunduh dari sumber otentik, atau ikon vektor dari library `lucide-react` / `heroicons`.

---

### Pola Slop #2: SVG Inline yang Cacat dan Tidak Proporsional

**Kesalahan:** AI Agent mencoba membuat SVG inline sendiri untuk merepresentasikan ikon kripto (BTC, ETH, ARB) langsung di dalam kode komponen. SVG yang dihasilkan cacat, tidak proporsional, dan tidak menyerupai logo resmi.

**Dampak:** Tampilan ikon terlihat amatir dan mencoreng kredibilitas visual platform Web3 institusional.

**Solusi yang Diterapkan:** Stop mengarang SVG inline dari nol untuk brand icon/logo aset kripto. Selalu unduh aset resmi dari sumbernya, lalu konversi ke WebP.

**Aturan untuk AI Agent berikutnya:** JANGAN PERNAH mengarang SVG inline untuk merepresentasikan logo kripto/brand eksternal. Selalu gunakan aset resmi.

---

### Pola Slop #3: Grid Simetris "Card Fatigue" (AI-Slop Layout)

**Kesalahan:** AI Agent menghasilkan tata letak landing page berupa grid 2-kolom atau 3-kolom simetris dengan kartu-kartu berukuran identik yang berisi konten teks generik tanpa densitas informasi yang nyata.

**Dampak:** Tampilan terasa seperti template website generik, tidak mencerminkan platform DeFi dengan data keuangan real-time. Developer secara eksplisit menolak pendekatan ini sebagai "AI-slop".

**Solusi yang Diterapkan:**
- Menerapkan **Asymmetric Bento Architecture** — kartu dengan ukuran berbeda (featured card lebih besar, auxiliary card lebih kecil).
- Mengadopsi bahasa desain **Bitget Exchange** (Tabbed Data Tables, Live Ticker Bar, Split Simulation Terminal, 3-Step Onboarding Sequence).
- Komponen `StatsOverview` diubah menjadi *Exchange Ticker-style metrics strip* bukan grid kartu statis.
- Komponen `TrendingMarketsTeaser` diubah menjadi *interactive tabbed data table* dengan baris data real-time (pool liquidity, probability bar, quick-bet buttons) bukan kartu grid.

**Aturan untuk AI Agent berikutnya:** HINDARI tata letak grid simetris berisi kartu-kartu identik. Selalu pertanyakan: "Apakah layout ini terlihat seperti platform DeFi/Web3 profesional, atau seperti template WordPress?" Jika jawabannya kedua, redesign dengan densitas data lebih tinggi dan hierarki visual yang asimetris.

---

### Pola Slop #4: Stacked Avatar Placeholder dengan Teks Hex Address

**Kesalahan:** AI Agent menggunakan elemen avatar bertumpuk (`0x1`, `0x4`, `0x9`) dengan warna latar solid berbeda-beda sebagai representasi "komunitas aktif" pada kartu metrik `StatsOverview.tsx`.

**Dampak:** Terlihat kaku, tidak proporsional, dan terasa seperti placeholder coding bootcamp bukan representasi komunitas Web3 institusional.

**Solusi yang Diterapkan:** Mengganti seluruh stacked avatar dengan ikon vektor tunggal yang bersih — SVG multi-user community icon yang ramping dan proporsional.

**Aturan untuk AI Agent berikutnya:** JANGAN gunakan elemen avatar berbasis teks hex singkat sebagai representasi visual komunitas. Gunakan ikon vektor yang bersih atau indikator numerik yang tepat.

---

### Pola Slop #5: Layout Shift / Blink saat Pergantian Tab

**Kesalahan:** Komponen `TrendingMarketsTeaser` menampilkan jumlah baris pasar yang berbeda per tab (9 baris di "Hot Markets", 3 baris di "Crypto/L2/Macro"). Saat pengguna berada di posisi scroll bawah dan berpindah tab, tinggi kontainer runtuh drastis sehingga posisi scroll "melompat" ke atas — menghasilkan efek kedip/blink yang mengganggu.

**Solusi yang Diterapkan:**
1. Menyelaraskan jumlah pasar yang ditampilkan per tab sehingga tinggi kontainer konsisten.
2. Menerapkan `min-h-[460px]` kemudian `h-[460px] overflow-y-auto` untuk mengunci dimensi vertikal.
3. Menggunakan `transition-colors duration-150` (bukan `transition-all`) pada hover baris untuk mencegah animasi dimensi yang tidak perlu.
4. Menambahkan atribut `priority` pada seluruh `next/image` ikon tab agar decoding tidak memicu micro layout shift.

**Aturan untuk AI Agent berikutnya:** Setiap komponen yang merender konten dinamis dengan jumlah item berbeda antar state WAJIB menggunakan `min-height` atau `height` tetap untuk menghindari layout shift. Gunakan `transition-colors` atau `transition-[property]` yang terfokus, bukan `transition-all` pada elemen yang bisa berubah dimensi.

---

### Pola Slop #6: Inkonsistensi Gaya Badge Metrik antar Kartu

**Kesalahan:** Badge `3.0x Multiplier` pada kartu Points Distributed menggunakan warna emerald berbeda (`bg-[#34D399]/15 text-[#34D399] border border-[#34D399]/30`) dibandingkan badge `+24.6% this week` pada kartu Total Value Locked (`bg-yes-green/10 text-yes-green border border-yes-green/20`). Kedua badge merepresentasikan "metric yang positif" tetapi menggunakan token warna yang berbeda.

**Solusi yang Diterapkan:** Menyeragamkan kedua badge ke kelas `bg-yes-green/10 text-yes-green border border-yes-green/20` via token `yes-green` Tailwind yang konsisten dengan design system.

**Aturan untuk AI Agent berikutnya:** Selalu gunakan token warna semantik dari design system (`yes-green`, `no-red`, `warning-amber`) untuk badge status. JANGAN menggunakan nilai hex literal `#34D399` secara langsung jika sudah ada token yang setara — ini menciptakan inkonsistensi visual yang sulit di-audit.

---

### Pola Slop #7: `@utility` Pseudo-Element Tailwind v4 yang Tidak Valid

**Kesalahan:** AI Agent mencoba mendefinisikan `@utility bitget-tab-active::after { ... }` di dalam `globals.css` menggunakan sintaks Tailwind v4 `@utility`. Tailwind v4 tidak mengizinkan pseudo-element (`::after`, `::before`) didefinisikan langsung di dalam nama `@utility` — ini hanya valid untuk class alphanumerik biasa.

**Dampak:** Error `CssSyntaxError: @utility bitget-tab-active::after defines an invalid utility name` yang menghentikan seluruh *dev server*.

**Solusi yang Diterapkan:** Memindahkan definisi `::after` ke dalam class CSS biasa di luar blok `@utility`:
```css
.bitget-tab-active { position: relative; }
.bitget-tab-active::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0; right: 0;
  height: 2px;
  background: #34D399;
  border-radius: 9999px;
  box-shadow: 0 0 12px rgba(52, 211, 153, 0.8);
}
```

**Aturan untuk AI Agent berikutnya:** Di Tailwind CSS v4, `@utility <name>` HANYA berlaku untuk nama class alphanumerik tanpa pseudo-element atau pseudo-class. Untuk mendefinisikan `::after`, `::before`, `:hover`, `::placeholder`, dll., gunakan CSS class biasa di luar blok `@utility`.

---

*(Catatan retrospective berikutnya ditambahkan di atas baris ini)*
