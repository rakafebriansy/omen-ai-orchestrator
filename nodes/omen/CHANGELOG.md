# CHANGELOG — Omen

Changelog berfungsi sebagai catatan riwayat perubahan untuk node **Omen**.

## Kategori Perubahan

*   **Guideline: <judul>**: Perubahan atau penambahan pada dokumen panduan.
*   **PRD**: Perubahan pada Product Requirements Document.
*   **Design System**: Pembaruan atau modifikasi Design System.
*   **System Design**: Perubahan pada arsitektur atau System Design.
*   **Development Planning: <nomor>**: Pembaruan pada perencanaan pengembangan.
*   **Ticket: <nomor>**: Perbaikan atau penambahan fitur yang merujuk pada tiket tertentu.
*   **Prototype: <judul>**: Pembaruan atau pembuatan prototipe desain/aplikasi.
*   **Implementation**: Implementasi coding pada codebase aplikasi.

## Log Perubahan (Omen)

*(⚠️ PERHATIAN AI AGENT: TAMBAHKAN ENTRI LOG BARU ANDA TEPAT DI BAWAH BARIS INI. JANGAN DI PALING BAWAH DOKUMEN!)*

### [2026-09-16 14:02:00] - Implementation: TICKET-12 Pembuatan Komponen Filter Kategori Pasar Prediksi
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 7-20 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> buatlah permintaan add commit dan push -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Mengembangkan komponen filter navigasi kategori dan pengurutan pasar prediksi `MarketCategoryFilter`:
  1. `MarketCategoryFilter.tsx`: `[Created]` Membangun komponen filter pill kategori horizontal (*All Markets, Trending, Crypto Narratives, Meme Tokens, Closing Soon, Resolved*), input teks pencarian judul pasar dengan ikon SVG & tombol clear, serta dropdown sort opsi pengurutan (*Highest Pool, Ending Soonest, Newest*) yang responsif, mobile-scrollable, dan theme-aware.
  2. `market-filter.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 5 pengujian mencakup verifikasi rendering pill kategori, perpindahan kategori aktif, pengetikan & pembersihan query pencarian, perubahan opsi sort, dan badge jumlah market (total 60/60 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/components/MarketCategoryFilter.tsx`, `omen/web/tests/market-filter.test.tsx`, `nodes/omen/tickets/TICKET-12-market-category-filter-ui.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:58:00] - Implementation: TICKET-11 Pembuatan Halaman Leaderboard Poin
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 7-20 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> buatlah permintaan add commit dan push -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Membangun halaman penuh Points Leaderboard di rute `app/leaderboard/page.tsx`:
  1. `app/leaderboard/page.tsx`: `[Created]` Memadukan header kompetisi Season 1, kartu ringkasan personal ranking (Rank `#4`, Total Points `52,300 PTS`, Gap to Next Tier `+29,100 PTS to #3`), input pencarian instan filter ENS/0x address dompet, serta integrasi komponen `<LeaderboardTable />` berstandar Web3 institusional yang sepenuhnya responsif dan theme-aware.
  2. `leaderboard-page.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 3 pengujian mencakup rendering header & 3 kartu personal stats, penyaringan pencarian ENS/address secara real-time, dan delegasi paginasi (total 55/55 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/app/leaderboard/page.tsx`, `omen/web/tests/leaderboard-page.test.tsx`, `nodes/omen/tickets/TICKET-11-points-leaderboard-page.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:54:00] - Implementation: TICKET-10 Pembuatan Tabel Ranking Leaderboard Poin
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 7-20 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> buatlah permintaan add commit dan push -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Mengembangkan komponen tabel peringkat leaderboard poin `LeaderboardTable`:
  1. `LeaderboardTable.tsx`: `[Created]` Membangun komponen tabel peringkat ranking global trader dengan visualisasi podium 1-3 (*Gold 🥇, Silver 🥈, Bronze 🥉*), avatar inisial/ENS domain, badge streak hari (*🔥 Xd*), tier multiplier, format poin (`+PTS`), penandaan kontras baris pengguna aktif (*Current User / YOU*), serta kontrol navigasi paginasi (*Previous/Next*) yang responsif dan theme-aware.
  2. `leaderboard-table.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 4 pengujian mencakup verifikasi struktur tabel, render badge podium 1-3, highlight pengguna aktif, dan fungsi navigasi tombol paginasi (total 52/52 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/components/LeaderboardTable.tsx`, `omen/web/tests/leaderboard-table.test.tsx`, `nodes/omen/tickets/TICKET-10-points-leaderboard-table-ui.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:51:00] - Implementation: TICKET-09 Pembuatan Halaman Quests dan Farming
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 7-20 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> buatlah permintaan add commit dan push -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Membangun halaman penuh Quests & Points Farming di rute `app/quests/page.tsx`:
  1. `app/quests/page.tsx`: `[Created]` Memadukan header kampanye Season 1, kartu ringkasan saldo poin total (`2,450 PTS`), status ranking tier (*Tier II • Silver Hunter*), stat boxes (Quests Done, Active Streak, Airdrop Rank), `<DailyCheckinWidget />`, serta direktori katalog misi berfitur filter tab kategori interaktif (*All Quests, Onboarding, Social, On-Chain, Daily*) yang terhubung dengan update saldo poin live.
  2. `quests-page.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 4 pengujian mencakup verifikasi render elemen halaman, penyaringan tab kategori misi, dan kalkulasi pertambahan poin saat quest diselesaikan (total 48/48 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/app/quests/page.tsx`, `omen/web/tests/quests-page.test.tsx`, `nodes/omen/tickets/TICKET-09-quests-farming-page.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:48:00] - Implementation: TICKET-08 Pembuatan Komponen Kartu Quest
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 7-20 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> buatlah permintaan add commit dan push -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Mengembangkan komponen baris/kartu misi `QuestCard` untuk modul gamifikasi:
  1. `QuestCard.tsx`: `[Created]` Membangun komponen kartu tugas dengan tag kategori semantik (*Social, Onboarding, On-Chain, Daily*), judul instruksi misi, deskripsi, reward points badge (`+PTS`), dan 3 status tombol (*Available*, *Verifying spinner*, dan *Completed check badge*) yang responsif dan theme-aware.
  2. `quest-card.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 4 pengujian mencakup rendering informasi misi, transisi verifikasi asynchronous, disabled verifying state, dan completed state (total 44/44 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/components/QuestCard.tsx`, `omen/web/tests/quest-card.test.tsx`, `nodes/omen/tickets/TICKET-08-quest-list-cards-ui.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:43:00] - Implementation: TICKET-07 Pembuatan Widget Daily Check-in Streak
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 7-20 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> buatlah permintaan add commit dan push -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Mengembangkan komponen widget gamifikasi streak reward harian `DailyCheckinWidget`:
  1. `DailyCheckinWidget.tsx`: `[Created]` Membangun kalender matriks visual 7 hari dengan pembagian status interaktif (*Claimed/Checked*, *Today Active*, *Locked/Upcoming*), badge pengganda streak aktif (*Multiplier Active*), tombol aksi klaim reward harian, notifikasi perolehan poin instan, serta live timer countdown cooldown (*Next Check-in in HHh MMm SSs*) yang theme-aware dan aksesibel.
  2. `checkin-widget.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 3 pengujian mencakup verifikasi grid status, eksekusi tombol klaim poin harian, transisi cooldown timer, dan initial cooldown rendering (total 40/40 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/components/DailyCheckinWidget.tsx`, `omen/web/tests/checkin-widget.test.tsx`, `nodes/omen/tickets/TICKET-07-daily-checkin-widget-ui.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:37:00] - Implementation: TICKET-06 Pembuatan Dialog Network Switcher Phantom EVM
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan ticket 6-10 dengan workflow: buat implementation plan -> saya proceed -> kerjakan -> testing -> linter -> beritahu informasi terkait apa yang diubah untuk saya cek manual -> repeat untuk task berikutnya"
- **Perubahan:** `[Added]` Membangun komponen dialog modal peringatan wrong network `NetworkSwitcherModal` dan indikator status jaringan pada header navigasi:
  1. `NetworkSwitcherModal.tsx`: `[Created]` Mengembangkan dialog modal peringatan dengan ikon amber berkilau, kartu status jaringan perbandingan aktif (Ethereum Mainnet) vs target (Arbitrum Sepolia Chain ID 421614), animasi loading pada tombol switch, opsi dismiss/close, serta atribut aksesibilitas WAI-ARIA (`role="dialog"`, `aria-modal="true"`, `aria-labelledby`, `aria-describedby`).
  2. `Navbar.tsx`: `[Updated]` Menambahkan badge peringatan "Wrong Network" berdenyut (*animate-ping*) di samping tombol wallet saat rantai tidak sesuai, yang memicu dialog modal switcher ketika diklik.
  3. `network-switcher.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 5 pengujian (total 37/37 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy dan type check TypeScript terverifikasi.
- **Path File:** `omen/web/components/NetworkSwitcherModal.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/tests/network-switcher.test.tsx`, `nodes/omen/tickets/TICKET-06-network-switcher-dialog-ui.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:27:00] - Implementation: TICKET-05 Pembuatan Komponen Tombol Connect Wallet
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan TICKET-05-connect-wallet-button-ui.md"
- **Perubahan:** `[Added]` Membangun komponen UI tombol dompet Web3 `ConnectWalletButton` dan mengintegrasikannya ke dalam layout header navigasi:
  1. `ConnectWalletButton.tsx`: `[Created]` Mengembangkan komponen interaktif dengan 3 status (Disconnected, Connecting, Connected), representasi visual saldo ETH (`0.45 ETH`), chip alamat terpotong (`0x1234...5678`) dengan green status pulse dot, menu dropdown interaktif (Copy Address dengan feedback sementara "Copied!" 2s, View on Explorer ke Arbiscan Sepolia, Disconnect), outside-click listener, dan kelengkapan WAI-ARIA accessibility (`aria-haspopup`, `aria-expanded`, `aria-label`).
  2. `Navbar.tsx`: `[Updated]` Mengintegrasikan komponen `ConnectWalletButton` pada baris navigasi desktop dan drawer navigasi mobile menggantikan tombol statis.
  3. `wallet-button.test.tsx`: `[Created]` Menyusun test suite unit testing Vitest 8 pengujian mencakup seluruh transisi status, interaksi dropdown, clipboard copy, link explorer, dan event disconnect (total 32/32 tests pass 100% pada suite Vitest). Kepatuhan mutlak Zero-Comment Policy terverifikasi.
- **Path File:** `omen/web/components/ConnectWalletButton.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/tests/wallet-button.test.tsx`, `nodes/omen/tickets/TICKET-05-connect-wallet-button-ui.md`, `nodes/omen/CHANGELOG.md`



### [2026-09-16 13:18:00] - Guideline: Pembuatan Prompt Logo Aplikasi Omen & Pembaruan Retrospective Slop
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "dari omen-ai-orchestrator dan omen-dir buatlah prompt untuk logo aplikasi. prompt saja"
- **Perubahan:**
  1. `[Created]` Menyusun prompt desain logo berformat production-grade untuk aplikasi **Omen** berdasarkan dokumen `design-system.md` dan `prd.md` — mencakup spesifikasi: symbol orb oracle dengan vertical emerald split, wordmark uppercase font mono institusional, palet `#030906` / `#10B981` / `#34D399`, tone *Institutional Web3 / DeFi-grade*, dan tiga varian (dark, light, square favicon).
  2. `[Updated]` Mencatat retrospective pembelajaran penting terkait pencegahan *AI-generated slop* (konten generik-simetris, card fatigue, emoji ikon) ke dalam `RETROSPECTIVE.md` agar AI agent berikutnya tidak mengulangi kesalahan desain serupa.
- **Path File:** `nodes/omen/CHANGELOG.md`, `nodes/omen/retrospectives/RETROSPECTIVE.md`


### [2026-09-16 12:37:00] - Implementation: Sinkronisasi Gaya Badge Stats & Fitur Scrollable pada Tabel Trending Prediction Markets
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "1. +24.6% this week di TOTAL VALUE LOCKED dan 3.0x Multiplier di POINTS DISTRIBUTED samakan stylenya; 2. di tabel Trending Prediction Markets buatlah scrollable, heightnya mengunakan height saat ini"
- **Perubahan:** `[Updated]` Menyelaraskan desain visual dan fungsionalitas scroll internal:
  1. Menyamakan gaya badge metrik `3.0x Multiplier` pada kartu Points Distributed di `StatsOverview.tsx` menjadi `text-[11px] font-bold px-2 py-0.5 rounded bg-yes-green/10 text-yes-green border border-yes-green/20`, identik dengan badge `+24.6% this week` pada kartu Total Value Locked.
  2. Menerapkan `h-[460px] overflow-y-auto custom-scrollbar` pada kontainer daftar pasar di `TrendingMarketsTeaser.tsx` dan menambahkan utilitas `.custom-scrollbar` bertema emerald halus pada `globals.css` sehingga tabel dapat digulir secara vertikal tanpa mengubah tinggi dokumen atau memicu layout shift.
- **Path File:** `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/app/globals.css`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 12:33:00] - Implementation: Variasi Data Pasar per Tab (5 4 1 2) & Stabilitas Tata Letak Dinamis pada Trending Prediction Markets
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "buatlah data tab beragam coba, 5 4  1 2"
- **Perubahan:** `[Updated]` Mengonfigurasi distribusi data pasar terkurasi yang variatif di tiap kategori tab pada `TrendingMarketsTeaser.tsx`:
  1. *Hot Markets*: 5 pasar teratas (Ethereum $4,500, Bitcoin $120k, Arbitrum DAU 1.5M, Crypto Cap $3.5T, US Fed Rate Cut).
  2. *Crypto*: 4 pasar (Ethereum $4,500, Bitcoin $120k, Solana DEX Volume Flip, Bitcoin Dominance 60%).
  3. *Layer 2*: 1 pasar unggulan (Arbitrum DAU 1.5M).
  4. *Macro*: 2 pasar (Crypto Cap $3.5T, US Fed Rate Cut).
  5. Menambahkan kontainer stabil `min-h-[460px]` dengan callout kartu "Propose New Market +" untuk kategori dengan data ringkas (≤ 2 pasar), memastikan tidak ada lonjakan tinggi atau pergeseran layout saat berganti antar tab.
- **Path File:** `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 12:30:00] - Implementation: Eliminasi Layout Shift & Blink saat Pindah Tab pada Trending Prediction Markets
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "saat pindah tab di Trending Prediction Markets, ada blink saat di paling bawah"
- **Perubahan:** `[Updated]` Menghilangkan layout shift, lonjakan tinggi kontainer (*height jump*), dan kedipan (*blink*) saat berganti tab di `TrendingMarketsTeaser.tsx`:
  1. Menyeragamkan kurasi pasar aktif menjadi 3 pasar unggulan terbaik per kategori (termasuk *Hot Markets*), sehingga tinggi kontainer konsisten 100% di semua tab.
  2. Menetapkan `min-h-[300px]` pada kontainer daftar pasar untuk stabilitas dimensi vertikal saat perpindahan state.
  3. Menambahkan atribut `priority` pada seluruh elemen ikon Next.js `Image` untuk menghindari *image decoding layout flash*.
  4. Mengganti `transition-all` yang memicu kalkulasi ulang dimensi menjadi `transition-colors duration-150` pada baris dan `transition-[width] duration-300` terfokus pada bar probabilitas YES/NO.
- **Path File:** `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 12:18:00] - Implementation: Perbaikan Gradasi Full-Bleed Light Mode & Eliminasi Boundary Cut pada Hero Section
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "di light mode ada warna gradasi tidak sesuai"
- **Perubahan:** `[Updated]` Memperbaiki percampuran gradasi warna latar belakang Light Mode pada `HeroSection.tsx` dan `globals.css`:
  1. Mengubah kontainer layer gambar dan overlay scrim dari `bottom-0 h-[68%]` menjadi `absolute inset-0` penuh, sehingga gradasi transisi mengalir mulus dan kontinu dari atas (putih bersih) ke bawah (mint-emerald lembut `#E2F7ED`) tanpa garis potongan horizontal melintang yang tajam.
  2. Menyesuaikan blending gambar 3D pada Light Mode menjadi `mix-blend-luminosity opacity-35` agar menyatu lembut dengan latar belakang tanpa bercak gelap.
  3. Menghaluskan garis pendaran atas `.light-emerald-seam` agar menyatu alami dengan kontainer rounded.
- **Path File:** `omen/web/components/landing/HeroSection.tsx`, `omen/web/app/globals.css`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 12:09:00] - Implementation: Penggantian Stacked Avatars dengan Ikon Komunitas Web3 Bersih
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "tertumpuk stacked, gunakan icon lain yang lebih baik"
- **Perubahan:** `[Updated]` Mengganti elemen avatar bertumpuk kaku (`0x1`, `0x4`, `0x9`) pada kartu Community Active di `StatsOverview.tsx` dengan ikon vektor komunitas (*multi-user network vector icon*) yang bersih, tajam, dan proporsional.
- **Path File:** `omen/web/components/landing/StatsOverview.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 12:06:00] - Implementation: Restrukturisasi Layout Kompak & Hierarki Visual Jernih pada Stats Overview Cards
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "dalam satu kartu buatlah informasinya tetap compact namun mudah dilihat. saat ini sangat buruk penempatan layoutnya"
- **Perubahan:** `[Updated]` Merestrukturisasi tata letak 4 kartu metrik pada `StatsOverview.tsx` menjadi susunan grid modular 4-kolom yang ringkas, berhierarki tajam, dan mudah dipindai mata:
  1. *Header Row*: Label kategori dengan status denyut/ikon di sisi kiri dan badge jaringan/kategori di sisi kanan.
  2. *Hero Value*: Angka metrik utama masif `text-2xl sm:text-3xl font-black font-mono` dengan jarak vertikal yang lapang (*breathing room*).
  3. *Footer Row*: Border pembatas halus 1px memisahkan badge persentase/multiplier dengan keterangan status settlement.
- **Path File:** `omen/web/components/landing/StatsOverview.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 11:38:00] - Implementation: Pengayaan Data Pasar & Fungsionalitas Penuh Tab Filter pada Trending Prediction Markets
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "di Trending Prediction Markets buatlah tabbingnya berfungsi"
- **Perubahan:** `[Updated]` Mengembangkan fungsionalitas filter tab kategori (`Hot Markets`, `Crypto`, `Layer 2`, `Macro`) pada `TrendingMarketsTeaser.tsx` menjadi interaktif penuh dengan katalog 9 pasar prediksi biner terkurasi, badge hitungan dinamis untuk tiap kategori, indikator garis bawah aktif emerald, dan pemfilteran tabel seketika tanpa latensi.
- **Path File:** `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/tests/landing.test.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 11:33:00] - Implementation: Integrasi Ikon Kripto Asli WebP pada Trending Prediction Markets
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "svgnya cacat, cari png di internet lalu convert ke webp"
- **Perubahan:** `[Updated]` Mengunduh aset PNG resolusi tinggi untuk ikon kripto resmi (Bitcoin, Ethereum, Arbitrum), Hot/Flame, dan Macro Globe, mengonversinya ke format WebP terkompresi optimal dengan transparansi penuh (`cwebp -q 95 -alpha_q 100`), lalu mengintegrasikannya ke dalam komponen `TrendingMarketsTeaser.tsx` menggunakan komponen `next/image` untuk performa dan ketajaman visual maksimal.
- **Path File:** `omen/web/public/icons/btc.webp`, `omen/web/public/icons/eth.webp`, `omen/web/public/icons/arb.webp`, `omen/web/public/icons/hot.webp`, `omen/web/public/icons/macro.webp`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 11:27:00] - Implementation: Penggantian Emoji dengan Vector SVG Icon pada Trending Prediction Markets
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "gantilah icon icon di Trending Prediction Markets menjadi non emoji, tapi icon asli. seperti tab crypto menjadi icon btc dsb"
- **Perubahan:** `[Updated]` Mengganti seluruh emoji pada komponen `TrendingMarketsTeaser.tsx` dengan ikon vektor SVG kustom (Bitcoin `BtcIcon`, Arbitrum `ArbitrumIcon`, Flame `FlameIcon`, Macro Globe `MacroIcon`, dan Ethereum `EthIcon`) pada tab kategori dan badge pasar terdaftar. Memastikan estetika lebih profesional, tajam, dan konsisten di seluruh perangkat.
- **Path File:** `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 08:28:00] - Implementation: Transformasi Bahasa Desain Bitget Exchange (Tabbed Markets Table, Live Ticker Strip, Split Terminals, 3-Step Onboarding)
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "saya ingin konten dari landing page saya tidak hanya berupa card, gunakan https://www.bitget.com/ sebagai referensi. coba buka, screenshot dan implementasikan NAMUN HANYA STYLE NYA SAJA. SELURUH CONTENTNYA TETAP SEPERTI SAAT INI"
- **Perubahan:** `[Updated]` Mentransformasi tampilan landing page Omen (`omen/web/app/page.tsx`) dengan mengadopsi bahasa desain dan komponen interaktif berstandar Bitget Exchange tanpa mengubah seluruh konten Web3 Omen:
  1. `StatsOverview.tsx`: Mengubah kumpulan kotak bento menjadi *Live Exchange Ticker Bar & Protocol Metric Strip* dengan pembatas garis vertikal 1px dan indikator denyut data on-chain.
  2. `TrendingMarketsTeaser.tsx`: Mengubah kartu teaser menjadi *Interactive Tabbed Live Markets Table* dengan tab filter (`🔥 Hot Markets`, `💎 Crypto`, `⚡ Layer 2`, `📈 Macro`), meter probabilitas YES/NO, volume pool, dan tombol quick-bet instan di tiap baris.
  3. `FeaturePillars.tsx`: Mengubah pilar menjadi *Split Product Terminal Showcases* yang memadukan narasi protokol dengan *Trading Slip Simulator & Payout Calculator Widget* (Pillar I) dan *Streak Multiplier Vault* (Pillar II).
  4. `QuestsTeaser.tsx`: Mengadopsi tata letak *Task Center & Rewards Hub* dengan 7-day streak roadmap dan task list table berdensitas tinggi.
  5. `OnboardingJourney.tsx`: `[Added]` Membuat komponen alur onboarding berantai 3 langkah (`01 Connect Web3 Wallet` → `02 Claim Daily Quests` → `03 Predict & Earn Airdrop`).
  6. Pengujian Vitest bertambah menjadi 24 unit test lulus 100% dan Zero-Comment Policy terverifikasi.
- **Path File:** `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/components/landing/OnboardingJourney.tsx`, `omen/web/app/page.tsx`, `omen/web/app/globals.css`, `omen/web/tests/landing.test.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 08:05:00] - Implementation: Transformasi Asymmetric Bento Architecture dan Variasi Bentuk Kartu
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "terlalu ai slop, sebab terlalu simetris card-cardnya dan tidak ada bentuk lain dari card, buatlah asimetris"
- **Perubahan:** `[Updated]` Merombak susunan kartu yang monoton dan simetris menjadi arsitektur *Asymmetric Bento Matrix* dan variasi bentuk dinamis:
  1. `StatsOverview.tsx`: Bento grid 4-kolom asimetris (Hero TVL 2-kolom dengan on-chain live status + Active Markets 1-kolom dengan category badges + Points 1-kolom dengan multiplier badge + Community Wallets 4-kolom full-bleed ribbon dengan avatar stack).
  2. `FeaturePillars.tsx`: Asymmetric 60/40 Split (Pilar I 7-kolom lebar dengan simulasi gauge probabilitas binary Yes/No dan badge arsitektur Solidity; Pilar II 5-kolom vertikal dengan Streak Vault dan tier ladder reward).
  3. `TrendingMarketsTeaser.tsx`: 1 Kartu Spotlight Unggulan 7-kolom dengan odds meter besar dan tombol quick-bet + 2 Kartu Compact Bertumpuk 5-kolom.
  4. `QuestsTeaser.tsx`: 8-kolom timeline milestone perjalanan quest dengan highlight kartu emas Day 3 & Day 7 + 4-kolom panel status streak multiplier dan status airdrop eligibility.
  5. Pengujian 23 unit test Vitest 100% lulus dan kepatuhan Zero-Comment Policy terverifikasi.
- **Path File:** `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/tests/landing.test.tsx`, `nodes/omen/CHANGELOG.md`


### [2026-09-16 07:55:00] - Implementation: Penyelarasan Presisi Lebar Section dengan Navbar
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "panjang semua section di @page.tsx samakan dengan panjang navbar, saat ini semua section memiliki panjang yang kurang dari navbar"
- **Perubahan:** `[Updated]` Menyelaraskan struktur kontainer di `layout.tsx` dengan menyisipkan wrapper `max-w-[1400px] w-full mx-auto` di dalam `<main className="w-full px-4 sm:px-6 lg:px-8 xl:px-10">`, sehingga lebar seluruh section di `page.tsx` sejajar presisi 100% (*pixel-perfect match*) dengan panjang kontainer kartu Navbar di semua breakpoint layar.
- **Path File:** `omen/web/app/layout.tsx`, `nodes/omen/CHANGELOG.md`

### [2026-09-16 07:50:00] - Implementation: Penyeragaman Layout Hero Centered Stack dan Visual 3D Ribbon
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "susunan/layout hero (section pertama) nya antara light dan dark berbeda. buatlah sama dengan menggunakan yang dark mode, begitupun gambarnya"
- **Perubahan:** `[Updated]` Menyeragamkan susunan tata letak Hero Section di `HeroSection.tsx` pada Light Mode menjadi *Centered Stack Layout* yang identik 100% dengan Dark Mode (kicker badge Arbitrum Sepolia terpusat, Display H1 `clamp(42px, 7.5vw, 96px)` terpusat, subheadline terpusat, dan barisan CTA buttons terpusat). Menggunakan aset visual 3D liquid metal ribbons yang sama (`public/images/hero-dark-emerald.jpg`) di bagian bawah dengan *gradient scrim overlay* yang disesuaikan untuk masing-masing tema. Memperbarui unit testing di `tests/landing.test.tsx` (23 tests passing 100% pada Vitest).
- **Path File:** `omen/web/components/landing/HeroSection.tsx`, `omen/web/tests/landing.test.tsx`, `nodes/omen/CHANGELOG.md`

### [2026-09-16 07:45:00] - Implementation: Refinement Container Responsive dan Light Mode Glowing Shine
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "1. saat ini, tampilan landing page tidak fill the container. buatlah responsive sehingga fill the container 2. saat di light mode. di pinggir pinggir dari container beberapa konten, terdapat garis hijau, yang buruk dan annoying, tidak terlihat seperti kilauan, perbaikilah supaya menjadi kilauan seperti saat di darkmode"
- **Perubahan:** `[Updated]` Memperluas kontainer tata letak halaman agar mengisi seluruh lebar kanvas (`w-full max-w-[1400px] mx-auto px-4 sm:px-6 lg:px-8 xl:px-10`) di `layout.tsx`, `Navbar.tsx`, dan `Footer.tsx`, serta mengubah alignment flex di `page.tsx` menjadi `items-stretch w-full`. Menghilangkan seluruh garis hijau solid kaku pada Light Mode di `HeroSection.tsx`, `StatsOverview.tsx`, `FeaturePillars.tsx`, `TrendingMarketsTeaser.tsx`, `QuestsTeaser.tsx`, `AirdropBanner.tsx`, dan `Navbar.tsx`, menggantikannya dengan efek kilauan pendaran kaca mewah (*top seam glowing line* `light-emerald-seam` dan *specular glass shadow* `light-card-shine`).
- **Path File:** `omen/web/app/globals.css`, `omen/web/app/layout.tsx`, `omen/web/app/page.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/components/landing/HeroSection.tsx`, `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/components/landing/AirdropBanner.tsx`, `nodes/omen/CHANGELOG.md`

### [2026-09-16 07:30:00] - Implementation: TICKET-04 Dual Theme Dark Emerald dan Light Emerald Landing Page
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "berikut yang saya unggah adalah prompt kedua, dimana untuk membuat light mode dan dark mode, juga memperbaiki tampilan menjadi gradient background. ikutilah prompt tersebut dan sesuaikan dengan konteks app kita"
- **Perubahan:** `[Added]` Mengimplementasikan sistem tema ganda (Dark Emerald Mode dan Light Emerald Mode) pada Landing Page Hero dan ekosistem Web3 Omen. Menghasilkan dua aset 3D render fotorealistik (`public/images/hero-dark-emerald.jpg` dan `public/images/hero-light-emerald.png`), mengimplementasikan `ThemeProvider.tsx`, memperbarui `globals.css` dengan token warna Dark Emerald (`#030906`, `#0A0F0C`, `#34D399`, `#047857`) dan Light Emerald (`#CFF3E2`, `#A9EAC9`, `#0B1F16`, `#10221A`, `#0E7A4E`) beserta layered CSS gradients, merancang `HeroSection.tsx` dengan layout Centered Stack (Dark Mode) dan Left-Aligned Split (Light Mode), memperbarui `Navbar.tsx` dengan theme switcher toggle, serta menyelaraskan seluruh subkomponen (`StatsOverview.tsx`, `FeaturePillars.tsx`, `TrendingMarketsTeaser.tsx`, `QuestsTeaser.tsx`, `AirdropBanner.tsx`, `Footer.tsx`). Menambahkan unit testing di `tests/landing.test.tsx` dan `tests/navbar.test.tsx` (23 tests passing 100% pada Vitest).
- **Path File:** `omen/web/app/page.tsx`, `omen/web/app/layout.tsx`, `omen/web/app/globals.css`, `omen/web/components/ThemeProvider.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/components/landing/HeroSection.tsx`, `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/components/landing/AirdropBanner.tsx`, `omen/web/public/images/hero-dark-emerald.jpg`, `omen/web/public/images/hero-light-emerald.png`, `omen/web/tests/landing.test.tsx`, `omen/web/tests/navbar.test.tsx`, `nodes/omen/tickets/TICKET-04-landing-overview-page.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-16 06:40:00] - Implementation: TICKET-04 Landing Overview Page Dark Premium Hero
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "bacalah prompt di atas sebagai referensi style, buatkan landing page @page.tsx terbaik untuk konteks project web3 ini dengan kata kunci: betting, airdrop, crypto, gamification, quest"
- **Perubahan:** `[Added]` Mengimplementasikan Landing Page utama berestetika Dark Premium Luxury Hero (Wealthfront dan OpenZeppelin Style) di `omen/web` pada rute `app/page.tsx`. Menghasilkan aset 3D render fotorealistik (`public/images/hero-bg.jpg`), membuat komponen `HeroSection.tsx` dengan framed panel `#07090E`, glowing amber seam border, dan tipografi masif `clamp(42px, 7.5vw, 96px)`, `StatsOverview.tsx` dengan 4 metrik on-chain, `FeaturePillars.tsx` pilar ganda platform, `TrendingMarketsTeaser.tsx` dengan live odds Yes/No, `QuestsTeaser.tsx` dengan kalender 7-day streak dan instant tasks, serta `AirdropBanner.tsx` untuk kampanye airdrop Season 1. Menyelaraskan `Navbar.tsx` menjadi floating pill dan `globals.css` dengan latar true black `#000000`. Menambahkan unit testing di `tests/landing.test.tsx` (21 tests passing 100% pada Vitest).
- **Path File:** `omen/web/app/page.tsx`, `omen/web/components/landing/HeroSection.tsx`, `omen/web/components/landing/StatsOverview.tsx`, `omen/web/components/landing/FeaturePillars.tsx`, `omen/web/components/landing/TrendingMarketsTeaser.tsx`, `omen/web/components/landing/QuestsTeaser.tsx`, `omen/web/components/landing/AirdropBanner.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/app/globals.css`, `omen/web/public/images/hero-bg.jpg`, `omen/web/tests/landing.test.tsx`, `nodes/omen/tickets/TICKET-04-landing-overview-page.md`, `nodes/omen/CHANGELOG.md`


### [2026-09-15 23:10:00] - Implementation: TICKET-03 Layout Shell Navbar dan Footer
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan @TICKET-03-layout-shell-navbar-footer.md"
- **Perubahan:** `[Added]` Mengimplementasikan layout shell aplikasi berestetika OpenZeppelin Institutional Web3 di `omen/web`. Membuat komponen sticky `Navbar.tsx` dengan backdrop blur, logo Omen, badge status Testnet, deteksi rute aktif, slot tombol Connect Wallet, dan responsive hamburger drawer mobile. Membuat komponen `Footer.tsx` 4 kolom responsif (Brand dan indikator status Arbitrum Sepolia berdenyut, Platform, Developers, Community) beserta disclaimer. Mengintegrasikan `layout.tsx` dengan sticky footer layout. Menambahkan unit testing Vitest di `tests/navbar.test.tsx` dan `tests/footer.test.tsx` (15 tests passing, 100% test coverage).
- **Path File:** `omen/web/app/layout.tsx`, `omen/web/components/Navbar.tsx`, `omen/web/components/Footer.tsx`, `omen/web/tests/navbar.test.tsx`, `omen/web/tests/footer.test.tsx`, `nodes/omen/tickets/TICKET-03-layout-shell-navbar-footer.md`, `nodes/omen/CHANGELOG.md`


### [2026-09-15 22:50:00] - Testing: TICKET-02 Setup Testing Suite Vitest
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/wealthy-org/Omen.git`
- **Konteks:** "kerjakan @TICKET-02-setup-vitest-testing-suite.md"
- **Perubahan:** `[Added]` Mengonfigurasi test runner Vitest, `@testing-library/react`, `@testing-library/jest-dom`, `@vitejs/plugin-react`, dan jsdom di `omen/web`. Menambahkan konfigurasi `vitest.config.mts`, `tests/setup.ts`, sampel unit test `tests/sample.test.tsx`, serta script `npm run test`, `test:watch`, dan `test:coverage` di `package.json`.
- **Path File:** `omen/web/package.json`, `omen/web/package-lock.json`, `omen/web/vitest.config.mts`, `omen/web/tests/setup.ts`, `omen/web/tests/sample.test.tsx`, `nodes/omen/tickets/TICKET-02-setup-vitest-testing-suite.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-15 22:10:00] - Implementation: TICKET-01 Setup Next.js dan Tailwind v4 OpenZeppelin Theme
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/rakafebriansy/omen-ai-orchestrator.git`
- **Konteks:** "implementasikan @implementation_plan.md di branch main"
- **Perubahan:** `[Added]` Mengonfigurasi TypeScript (strict mode, `@/*` alias) dan Tailwind CSS v4 CSS-first (`@theme`) dengan palet tema OpenZeppelin Institutional Web3 di `omen/web`. Mengonversi `layout.js` dan `page.js` menjadi `layout.tsx` dan `page.tsx`, menambahkan `postcss.config.mjs`, serta membersihkan file lama `page.module.css` dan `jsconfig.json`.
- **Path File:** `omen/web/package.json`, `omen/web/tsconfig.json`, `omen/web/postcss.config.mjs`, `omen/web/app/globals.css`, `omen/web/app/layout.tsx`, `omen/web/app/page.tsx`, `nodes/omen/tickets/TICKET-01-setup-nextjs-tailwind-theme.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-15 19:51:00] - Design System: OpenZeppelin Theme Migration
> **Trigger:** Prompt Driven | **Branch:** `main` | **Repo:** `https://github.com/rakafebriansy/omen-ai-orchestrator.git`
- **Konteks:** "ganti tema nya dari cyberpunk ke seperti web ini: https://www.openzeppelin.com/solidity-contracts?ref=landingfolio"
- **Perubahan:** `[Changed]` Memperbarui seluruh pedoman visual dan token desain dari tema Cyberpunk Glassmorphism menjadi **OpenZeppelin Institutional Web3 / Developer-First Aesthetic** (Clean White `#FFFFFF` surface, Slate `#0F172A`, Royal Cobalt `#4E5EE4`, Emerald `#10B981`, Rose `#F43F5E`, crisp 1px borders, typography Inter + JetBrains Mono). Menyelaraskan dokumen `global-docs/design-system.md`, `global-docs/ui-example.md`, `global-docs/prd.md`, `nodes/omen/guidelines/project-context.md`, `nodes/omen/docs/system-design.md`, dan tiket terkait (`TICKET-01`, `TICKET-08`).
- **Path File:** `global-docs/design-system.md`, `global-docs/ui-example.md`, `global-docs/prd.md`, `nodes/omen/guidelines/project-context.md`, `nodes/omen/docs/system-design.md`, `nodes/omen/tickets/TICKET-01-web-typescript-tailwind-setup.md`, `nodes/omen/tickets/TICKET-08-points-leaderboard-ui.md`, `nodes/omen/CHANGELOG.md`

### [2026-09-15 15:31:00] - Initialization: Single-Project Environment Node Setup
> **Trigger:** Autonomous Planning | **Branch:** `main` | **Repo:** `https://github.com/rakafebriansy/omen-ai-orchestrator.git`
- **Konteks:** "Saya ingin menginisialisasi Single-Project Environment menggunakan kerangka kerja AI Orchestrator ini. Nama Sistem: Omen. Mode 1 (Autonomous Planning)."
- **Perubahan:** `[Added]` Menginisialisasi node utama `nodes/omen/` untuk sistem Points/Quest Farming + Prediction Market Dashboard Omen. Membuat dokumen fondasi terisolasi mencakup `nodes/omen/main.md` dengan status aktif MODE 1, `nodes/omen/guidelines/project-context.md` dari hasil pemindaian struktur monorepo (`omen/contracts` & `omen/web`), `nodes/omen/docs/system-design.md` beserta 4 diagram arsitektur PlantUML (`erd.puml`, `flowchart.puml`, `state-diagram.puml`, `sequence-diagram.puml`), `nodes/omen/docs/development-planning.md` dengan 12 tiket backlog Fase 1 (`TICKET-01` s/d `TICKET-12`), dan menyelaraskan `global-docs/prd.md` serta `global-docs/design-system.md` dan diagram global (`user-journey.puml`, `use-case.puml`).
- **Path File:** `nodes/omen/main.md`, `nodes/omen/CHANGELOG.md`, `nodes/omen/guidelines/project-context.md`, `nodes/omen/docs/system-design.md`, `nodes/omen/docs/development-planning.md`, `nodes/omen/tickets/TICKET-01-web-typescript-tailwind-setup.md`, `nodes/omen/tickets/TICKET-02-hardhat-smart-contract-setup.md`, `nodes/omen/tickets/TICKET-03-supabase-schema-migration.md`, `nodes/omen/tickets/TICKET-04-prediction-market-contract.md`, `nodes/omen/tickets/TICKET-05-contract-unit-testing.md`, `nodes/omen/tickets/TICKET-06-wallet-connect-wagmi.md`, `nodes/omen/tickets/TICKET-07-daily-checkin-quest-api.md`, `nodes/omen/tickets/TICKET-08-points-leaderboard-ui.md`, `nodes/omen/tickets/TICKET-09-prediction-market-list-ui.md`, `nodes/omen/tickets/TICKET-10-betting-claim-flow.md`, `nodes/omen/tickets/TICKET-11-admin-market-resolver.md`, `nodes/omen/tickets/TICKET-12-testnet-e2e-deployment.md`, `nodes/omen/docs/diagrams/erd.puml`, `nodes/omen/docs/diagrams/flowchart.puml`, `nodes/omen/docs/diagrams/state-diagram.puml`, `nodes/omen/docs/diagrams/sequence-diagram.puml`, `global-docs/prd.md`, `global-docs/design-system.md`, `global-docs/diagrams/user-journey.puml`, `global-docs/diagrams/use-case.puml`
