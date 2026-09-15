# Product Requirements Document (PRD) — Omen

## 1. Tujuan & Latar Belakang (*Objective & Background*)

### 1.1 Latar Belakang Masalah
Dalam ekosistem Web3, komunitas pengguna sering terbagi menjadi dua minat besar: pemburu *airdrop / quest farming* yang gemar menyelesaikan tugas harian demi akumulasi poin, dan trader *degen* yang aktif berpartisipasi dalam *prediction market* on-chain. Banyak platform memisahkan kedua utilitas ini, sehingga menyulitkan proyek baru untuk mempertahankan keterlibatan (*retention*) pengguna harian sekaligus menghasilkan volume transaksi on-chain yang nyata.

### 1.2 Solusi Produk: Omen
**Omen** adalah platform terpadu yang menggabungkan dua pilar utama dalam satu token dan ekosistem:
1. **Points & Quest Farming Engine:** Pengguna mendapatkan poin dari check-in harian (*streak counter*), penyelesaian misi/tugas, dan referral.
2. **Crypto & Meme Prediction Market:** Pasar prediksi on-chain bertema tren crypto (misal: "Apakah token X naik >20% minggu ini?") di mana partisipasi taruhan (menang maupun kalah) secara langsung memberikan poin aktivitas.

### 1.3 Target Pengguna (*User Personas*)
1. **Airdrop / Points Farmers:** Pengguna yang aktif melakukan interaksi harian untuk mengumpulkan poin demi peringkat leaderboard dan potensi hadiah airdrop di masa depan.
2. **Prediction Market Bettors / Crypto Degens:** Trader yang gemar memasang taruhan cepat dua arah (Yes/No) pada narasi atau tren token crypto dengan kepastian pembayaran proporsional.
3. **Project Administrator / Operator:** Pengelola ekosistem yang mengatur pembuatan quest baru, peluncuran market baru, dan resolusi hasil pasar secara transparan.

---

## 2. Alur Pengguna (*User Flow / User Journey*)

Alur pengalaman pengguna mencakup tahap eksplorasi landing page, koneksi Phantom Wallet (EVM mode), klaim check-in harian, penjelajahan quest, pemasangan taruhan on-chain, pengecekan peringkat leaderboard, hingga klaim payout kemenangan.

* **Visualisasi PlantUML User Journey:** [user-journey.puml](./diagrams/user-journey.puml)

---

## 3. Interaksi Sistem Global (*Use Case Diagram*)

Interaksi antara aktor Pengguna (*Farmer/Bettor*), Administrator, dan Smart Contract Indexer.

* **Visualisasi PlantUML Use Case:** [use-case.puml](./diagrams/use-case.puml)

---

## 4. Kebutuhan Fungsional (*Functional Requirements*)

### 4.1 Autentikasi & Koneksi Wallet
- Pengguna menghubungkan dompet menggunakan Phantom Wallet dalam mode EVM via pustaka `wagmi` dan `viem`.
- Sistem secara otomatis mendaftarkan atau memperbarui rekam jejak pengguna di basis data Supabase (`/api/wallet/connect`).

### 4.2 Daily Check-in & Streak Counter
- Pengguna dapat melakukan klaim poin harian (*Daily Check-in*) satu kali setiap 24 jam per alamat dompet.
- Sistem mencatat penghitung beruntun (*streak counter*); check-in berturut-turut memberikan pengali (*bonus multiplier*) poin.

### 4.3 Quest & Task Engine
- Sistem menampilkan daftar misi aktif (misal: "Connect Wallet Pertama Kali", "Ikut 1 Prediction Market", "Follow Akun X Resmi", "Ajak Teman via Referral").
- Pengguna dapat memicu verifikasi penyelesaian tugas (`/api/quests/:id/complete`); poin langsung dialokasikan ke saldo pengguna.

### 4.4 Points Leaderboard
- Papan peringkat global yang menyajikan ranking seluruh alamat dompet berdasarkan akumulasi total poin.
- Kartu informasi personal di bagian atas untuk melihat posisi peringkat pengguna saat ini dan selisih poin ke tier terdekat.

### 4.5 Prediction Market Listing & Odds Display
- Menampilkan daftar pasar prediksi aktif dengan filter kategori (Trending, Crypto, Meme, Closing Soon, Resolved).
- Kartu pasar menampilkan judul prediksi, batas waktu penutupan (*deadline*), total pool Yes vs No, rasio persentase probabilitas (*implied odds*), dan status pasar.

### 4.6 On-Chain Betting Flow (Native ETH)
- Pengguna memilih sisi (Yes / No), memasukkan nominal taruhan dalam Native ETH (Arbitrum Sepolia / Robinhood Chain testnet), dan menyetujui transaksi melalui dompet.
- Dana taruhan dikelola langsung oleh smart contract `PredictionMarket.sol` tanpa perantara kustodian backend.
- Event transaksi on-chain di-index ke basis data Supabase (`/api/bets/index`) sekaligus memberikan bonus poin partisipasi.

### 4.7 Klaim Kemenangan (*Claim Payout*)
- Setelah pasar ditutup dan di-resolve oleh admin, pengguna yang bertaruh pada sisi pemenang dapat mengeksekusi fungsi `claim()` pada smart contract.
- Payout dibagikan secara proporsional dari total pool lawan yang kalah.

### 4.8 Panel Administrator (*Admin Panel*)
- Halaman terisolasi yang diproteksi secara ketat: hanya alamat dompet yang terdaftar pada `ADMIN_WALLET_ADDRESS` yang dapat mengakses.
- Fungsionalitas admin:
  - Membuat quest baru atau menonaktifkan quest yang sudah lewat masa berlakunya.
  - Mendaftarkan pasar prediksi baru (memicu `createMarket()` di kontrak lalu menyimpan metadata ke Supabase).
  - Melakukan resolusi hasil pasar (`resolveMarket()` di kontrak dengan hasil Yes/No).

---

## 5. Kebutuhan Non-Fungsional (*Non-Functional Requirements*)

1. **Keamanan Dana (Non-Custodial):** Seluruh aliran dana taruhan dan klaim kemenangan dieksekusi murni secara on-chain di smart contract. Backend tidak pernah menyimpan *private key* atau menampung dana pengguna.
2. **Aksesibilitas (a11y):**
   - Kepatuhan kontras warna **WCAG 2.1 AA** (terutama untuk elemen teks di atas latar belakang gelap, kartu taruhan Yes/No, dan badge status).
   - **ARIA Screen Reader Labels** pada indikator streak, tombol toggle Yes/No, bilah persentase pool, dan saldo poin.
3. **Kebijakan Testnet-First:** Seluruh pengujian dan simulasi smart contract **WAJIB** tuntas di testnet (Arbitrum Sepolia / Robinhood Chain Testnet) sebelum diluncurkan ke lingkungan mainnet.
4. **Performa Antarmuka:** Waktu rendering halaman awal < 1.5 detik dengan optimasi Server-Side Rendering (SSR) Next.js 14+ App Router dan caching Supabase.

---

## 6. Kriteria Penerimaan (*Acceptance Criteria / Definition of Done*)

- [x] Alur Daily Check-in, Quest list, dan Points Leaderboard beroperasi mulus tanpa galat perolehan poin ganda.
- [x] Siklus penuh smart contract prediction market (Create -> Bet -> Resolve -> Claim) terbukti sukses dieksekusi end-to-end di testnet tanpa insiden dana macet.
- [x] Akses Admin Panel terkunci secara absolut bagi siapa pun selain `ADMIN_WALLET_ADDRESS`.
- [x] Tampilan antarmuka responsif dan selaras dengan panduan Design System bernuansa OpenZeppelin Institutional Web3 (Clean White & Slate theme).

---

## 7. Asumsi & Batasan Sistem (*Assumptions & Constraints*)

1. **Penyimpanan Poin Off-Chain (MVP):** Untuk efisiensi biaya gas dan kecepatan iterasi, data poin disimpan secara off-chain di Supabase. Jembatan token reward on-chain direncanakan pada Fase 2.
2. **Resolusi Manual Admin (MVP):** Resolusi pasar dilakukan secara manual oleh admin yang menyertakan catatan transparansi sumber data (oracle terdesentralisasi otomatis masuk ke Fase 2).
3. **Mata Uang Taruhan:** Menggunakan Native ETH pada rantai EVM yang didukung (Phantom EVM mode).

---

## 8. Di Luar Cakupan (*Out of Scope*)

- Oracle terdesentralisasi otomatis (Chainlink / Pyth integration) untuk penyelesaian instan (dialokasikan ke Fase 2).
- Sistem referral berjenjang multi-level (dialokasikan ke Fase 2).
- Audit formal keamanan smart contract oleh firma pihak ketiga (dijadwalkan sebelum peluncuran mainnet komersial).

---

## 9. Peta Jalan Rilis (*Milestones / Release Roadmap*)

- **Fase 1 (MVP — Milestone Saat Ini):**
  - Setup Next.js + TypeScript + Tailwind CSS & Hardhat.
  - Implementasi Smart Contract `PredictionMarket.sol` & unit tests 100% pass.
  - Skema Supabase (Users, Quests, Points Events, Markets, Bets).
  - Integrasi Phantom EVM Wallet via `wagmi`/`viem`.
  - UI & API: Daily Check-in Streak, Quest Engine, Leaderboard.
  - UI & Integrasi: Prediction Market Listing, Betting Flow, Claim Payout, Admin Panel.
  - Deployment & validasi E2E di Arbitrum Sepolia Testnet.
- **Fase 2 (Advanced Utilities):**
  - Sistem Referral Multiplier, Automated Price Feed Oracle, Leaderboard Win-Rate Prediktor Terbaik, Notifikasi penutupan pasar.
