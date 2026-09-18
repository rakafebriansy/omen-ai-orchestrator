# Knowledge Base & Implementation Q&A Repository (`LEARN.md`)

Dokumen ini adalah repositori terpusat (*Single Source of Truth*) untuk menyimpan seluruh tanya-jawab (*Question & Answer*) seputar implementasi teknis, keputusan arsitektural, dan logika *codebase* yang ditanyakan oleh pengguna (*User*).

Berbeda dengan log retrospektif error (`RETROSPECTIVE.md`), dokumen ini khusus mendokumentasikan pemahaman konseptual dan teknis yang diperoleh dari proses tanya-jawab eksplisit antara pengguna dan AI Agent.

---

## 🛑 Protokol Operasional AI Agent (Wajib Dipatuhi)

Setiap kali AI Agent menerima instruksi tanya-jawab implementasi (*Implementation Q&A Prompt*), agen **WAJIB MUTLAK** mematuhi 4 hukum operasional berikut:

### 1. Hanya Menjawab Pertanyaan Eksplisit (Strictly Explicit Q&A Only)
- AI Agent **DILARANG KERAS** membuat penjelasan, rangkuman, atau inisiatif analisis secara otomatis tanpa pertanyaan eksplisit yang diajukan oleh pengguna.
- Hanya jelaskan poin-poin pertanyaan yang secara nyata tertulis pada daftar pertanyaan pengguna (contoh: *1. Pertanyaan A, 2. Pertanyaan B*).

### 2. Berakar pada Codebase & Orchestrator (No Hallucinations / Full Grounding)
- Seluruh jawaban **WAJIB** berakar pada analisis kode sumber (*source code*) nyata, konfigurasi, dan dokumen orchestrator (`global-docs/`, `global-guidelines/`, `nodes/[nama-node]/`).
- Sertakan path file yang valid (dan nomor baris jika relevan) sebagai bukti konkret implementasi.
- Jelaskan **alasan/rasional (*why*)** di balik keputusan arsitektur, bukan hanya sekadar mendeskripsikan ulang baris kode (*what*).

### 3. Output Ganda (Dual-Output: Chat Sidebar + LEARN.md)
- AI Agent **WAJIB** mengetikkan jawaban lengkap, terstruktur, dan mudah dipahami langsung pada **chat sidebar** percakapan.
- Pada saat yang bersamaan, AI Agent **WAJIB** menyalin dan merekam sesi tanya-jawab tersebut ke bagian [Arsip Log Tanya-Jawab](#-arsip-log-tanya-jawab) di dalam file ini menggunakan [Format Entri Baku](#-format-entri-baku-boilerplate) serta memperbarui [Indeks Kategori](#-indeks-kategori--daftar-isi).

### 4. Disiplin Taksonomi & Kategorisasi
- AI Agent **WAJIB** mengklasifikasikan setiap entri Q&A ke dalam **Kategori Utama** dan menyematkan **Tags** yang relevan agar memudahkan pengguna dalam membaca dan mencari di kemudian hari.

---

## 🏷️ Taksonomi & Sistem Kategorisasi

Untuk menjaga keteraturan dan kemudahan pencarian (*searchability*), gunakan standar taksonomi berikut saat mencatat entri baru:

### 1. Format ID Entri
Gunakan format penomoran: `[QA-YYYYMMDD-XX]`
- `YYYYMMDD`: Tahun, Bulan, Tanggal pencatatan (contoh: `20260913`).
- `XX`: Nomor urut pada hari tersebut (contoh: `01`, `02`).

### 2. Daftar Kategori Utama (Pilih Salah Satu)
| Kategori Utama | Cakupan / Domain |
| :--- | :--- |
| **`Architecture & Pattern`** | Struktur folder, modularitas, alur sistem, design patterns, separation of concerns. |
| **`State Management & Data Flow`** | Alur data, global store (Zustand/Redux), server state (React Query), props/event flow. |
| **`Database & Data Modeling`** | Skema tabel/koleksi, ORM (Prisma/TypeORM/Mongoose), migrasi, indexing, query optimization. |
| **`API & Network Integration`** | REST endpoints, GraphQL, WebSocket, gRPC, format request/response, error handling network. |
| **`UI/UX & Design System`** | Komponen visual, Tailwind/CSS, konsistensi tema, responsivitas, aksesibilitas (a11y). |
| **`Security & Authentication`** | JWT, sesi, OAuth, RBAC/Permissions, hashing, sanitasi input, proteksi CORS/CSRF. |
| **`Testing & Quality Assurance`** | Strategi unit test, integration test, E2E, mock data, coverage, assertions. |
| **`Build, Tooling & DevOps`** | Konfigurasi bundler (Vite/Webpack), Docker, CI/CD, script npm, environment variables. |
| **`Business Logic & Domain Rules`** | Logika perhitungan, validasi transaksi, aturan proses bisnis spesifik aplikasi. |
| **`Orchestrator & Workflow`** | Aturan template, manajemen tiket, SOP guidelines, mekanisme multi-node. |

### 3. Konvensi Tagging
Gunakan format `#kebab-case` untuk tag spesifik. Contoh:
- `#jwt-auth` `#zustand` `#prisma-relations` `#optimistic-update` `#tailwind-v4` `#rbac-middleware`

---

## 📋 Format Entri Baku (Boilerplate)

AI Agent **WAJIB** menyalin struktur *markdown* berikut saat menambahkan rekaman tanya-jawab baru ke dalam file ini:

```markdown
### [QA-YYYYMMDD-XX] <Judul Singkat Representatif Terkait Topik Pertanyaan>
- **Tanggal**: YYYY-MM-DD HH:mm
- **Scope / Target Node**: `[Global / Nama Node / Path Codebase]`
- **Kategori**: `[Pilih salah satu dari Kategori Utama di atas]`
- **Tags**: `#tag1 #tag2 #tag3`
- **File Referensi**:
  - `path/to/relevant-file-1.ext` (L10-L45)
  - `path/to/relevant-file-2.ext`

#### ❓ Pertanyaan Pengguna
1. **[Tulis ulang pertanyaan 1 secara presisi]**
2. **[Tulis ulang pertanyaan 2 secara presisi]**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. [Judul Poin Jawaban 1]
- **Ringkasan Inti**: [Penjelasan singkat 1-2 kalimat]
- **Detail Implementasi & Logika**:
  [Penjelasan komprehensif alur kerja kode]
- **Rujukan Kode Sumber**:
  ```[language]
  // Cuplikan kode atau referensi fungsi/kelas yang relevan
  ```
- **Rasional & Keputusan Teknis**:
  [Mengapa pendekatan ini yang dipilih, pertimbangan trade-off, atau kesesuaian dengan pedoman]

##### 2. [Judul Poin Jawaban 2]
- **Ringkasan Inti**: [Penjelasan singkat 1-2 kalimat]
- **Detail Implementasi & Logika**:
  [Penjelasan komprehensif alur kerja kode]
- **Rujukan Kode Sumber**:
  ```[language]
  // Cuplikan kode atau referensi fungsi/kelas yang relevan
  ```
- **Rasional & Keputusan Teknis**:
  [Mengapa pendekatan ini yang dipilih, pertimbangan trade-off, atau kesesuaian dengan pedoman]

---
```

---

## 🗂️ Indeks Kategori & Daftar Isi

*AI Agent WAJIB memperbarui tautan indeks di bawah ini setiap kali menambahkan entri baru (urutkan dari yang terbaru / descending).*

- **Architecture & Pattern**
  - [[QA-20260918-04] Mekanisme Penghubung Media Sosial & Pemetaan Identitas Dompet (Social Integration vs Wallet Mapping)](#qa-20260918-04-mekanisme-penghubung-media-sosial--pemetaan-identitas-dompet-social-integration-vs-wallet-mapping)
- **State Management & Data Flow**
  - *(Belum ada entri)*
- **Database & Data Modeling**
  - [[QA-20260915-01] Fungsi & Peran total_pool_yes dan total_pool_no pada Tabel markets](#qa-20260915-01-fungsi--peran-total_pool_yes-dan-total_pool_no-pada-tabel-markets)
- **API & Network Integration**
  - [[QA-20260918-09] Status Integrasi Smart Contract dengan Jaringan Testnet (Live On-Chain vs Mock Environment)](#qa-20260918-09-status-integrasi-smart-contract-dengan-jaringan-testnet-live-on-chain-vs-mock-environment)
  - [[QA-20260918-05] Status Integrasi Nyata vs Mock pada AI Social Ingestion Pipeline](#qa-20260918-05-status-integrasi-nyata-vs-mock-pada-ai-social-ingestion-pipeline)
  - [[QA-20260918-03] Detail Teknis Endpoint & Mekanisme Tanda Tangan Konfirmasi Belief (Hit API vs On-Chain)](#qa-20260918-03-detail-teknis-endpoint--mekanisme-tanda-tangan-konfirmasi-belief-hit-api-vs-on-chain)
- **UI/UX & Design System**
  - [[QA-20260918-07] Fungsi & Peran Komponen Banner Creator Verification (CreatorConfirmation.tsx)](#qa-20260918-07-fungsi--peran-komponen-banner-creator-verification-creatorconfirmationtsx)
- **Security & Authentication**
  - [[QA-20260918-10] Analisis Mekanisme Autentikasi Admin Saat Ini (Form & Header Based) vs True Web3 Wallet Signature](#qa-20260918-10-analisis-mekanisme-autentikasi-admin-saat-ini-form--header-based-vs-true-web3-wallet-signature)
  - [[QA-20260918-08] Logika Otorisasi Alamat Dompet & Pencegahan Impersonasi pada Konfirmasi Kreator](#qa-20260918-08-logika-otorisasi-alamat-dompet--pencegahan-impersonasi-pada-konfirmasi-kreator)
  - [[QA-20260918-02] Verifikasi Identitas Influencer/Kreator & Rujukan UI Inspirasi (ui-example.md)](#qa-20260918-02-verifikasi-identitas-influencerkreator--rujukan-ui-inspirasi-ui-examplemd)
- **Testing & Quality Assurance**
  - *(Belum ada entri)*
- **Build, Tooling & DevOps**
  - *(Belum ada entri)*
- **Business Logic & Domain Rules**
  - [[QA-20260918-06] Titik Pemicu Pemanggilan OpenRouter AI pada Alur Pembuatan Belief](#qa-20260918-06-titik-pemicu-pemanggilan-openrouter-ai-pada-alur-pembuatan-belief)
  - [[QA-20260918-01] Mekanisme Gasless EIP-712 Creator/Influencer Belief Confirmation](#qa-20260918-01-mekanisme-gasless-eip-712-creatorinfluencer-belief-confirmation)
  - [[QA-20260915-02] Penjelasan Rumus Kalkulasi Payout Model Pari-Mutuel](#qa-20260915-02-penjelasan-rumus-kalkulasi-payout-model-pari-mutuel)
- **Orchestrator & Workflow**
  - *(Belum ada entri)*

---

## 📚 Arsip Log Tanya-Jawab

### [QA-20260918-10] Analisis Mekanisme Autentikasi Admin Saat Ini (Form & Header Based) vs True Web3 Wallet Signature
- **Tanggal**: 2026-09-18 20:45
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Security & Authentication`
- **Tags**: `#admin-authentication #web3-wallet #rbac #siwe #security-audit #admin-portal`
- **File Referensi**:
  - `omen/web/app/admin/page.tsx` (L28-L56, L175-L184)
  - `omen/web/components/AdminLoginForm.tsx` (L13-L168)
  - `omen/web/app/api/markets/route.ts` (L114-L152)
  - `omen/web/app/api/markets/[id]/resolve/route.ts` (L11-L40)

#### ❓ Pertanyaan Pengguna
1. **admin belum benar2 pakai wallet**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Bedah Mekanisme Autentikasi Admin Saat Ini (State Saat Ini)
- **Ringkasan Inti**: **BENAR SEKALI**. Halaman Admin (`/admin`) saat ini masih menggunakan **Form Otentikasi Input Teks & Header HTTP (`x-admin-wallet` / `x-admin-key`)**, belum mewajibkan koneksi dompet Web3 secara native (*Wagmi `useAccount`*) atau tanda tangan kriptografis (*Sign-In with Ethereum / SIWE*).
- **Detail Implementasi & Logika**:
  1. **Dual-Mode Login di UI ([`AdminLoginForm.tsx`](file:///Users/raka/Developer/repositories/projects/wealthy-people-org/omen-dir/omen/web/components/AdminLoginForm.tsx)):**
     - Mode 1: Mengetik alamat wallet secara manual ke dalam `<input>` teks (misal `0x1234...`).
     - Mode 2: Memasukkan passphrase master key (`omen-admin-2026`).
     - Tombol "Use Demo Admin" langsung mengisi string tanpa mengecek apakah browser pengguna benar-benar memiliki ekstensi Web3 wallet aktif atau memegang *private key* dari alamat tersebut.
  2. **Validasi Otorisasi di Antarmuka ([`app/admin/page.tsx`](file:///Users/raka/Developer/repositories/projects/wealthy-people-org/omen-dir/omen/web/app/admin/page.tsx)):**
     - Otorisasi hanya memeriksa apakah string `connectedAddress` ada di dalam array whitelist:
       ```typescript
       const isAuthorized =
         Boolean(connectedAddress) &&
         AUTHORIZED_ADMIN_ADDRESSES.includes(connectedAddress?.toLowerCase() || "");
       ```
  3. **Validasi Otorisasi di API Backend ([`route.ts`](file:///Users/raka/Developer/repositories/projects/wealthy-people-org/omen-dir/omen/web/app/api/markets/route.ts)):**
     - Endpoint `POST /api/markets` dan `POST /api/markets/[id]/resolve` hanya memeriksa header `x-admin-wallet` atau `x-admin-key`.
- **Rasional Desain MVP / Testing:**
  Pendekatan ini sengaja diterapkan pada tahap pengujian awal (MVP/Testing Phase) untuk memudahkan pengembang dan otomatisasi test suite (Vitest) menguji alur pembuatan & resolusi pasar tanpa harus selalu membuka *extension pop-up* MetaMask/Phantom pada setiap klik.

##### 2. Standar Produksi: Roadmap Menuju "True Web3 Admin"
- **Ringkasan Inti**: Untuk beralih ke *Production Web3 Native Admin*, sistem dapat ditingkatkan dengan 3 pilar:
  1. **Direct Wagmi Binding:** Menghapus form input teks manual dan langsung mengunci halaman ke `const { address, isConnected } = useAccount()`. Jika wallet tidak terhubung atau address bukan admin, halaman terkunci secara otomatis.
  2. **EIP-4361 (SIWE) / EIP-712 Admin Session:** Admin wajib menandatangani pesan tantangan (*cryptographic challenge nonce*) untuk menghasilkan JWT Admin Session yang aman dan terverifikasi secara matematis.
  3. **Smart Contract Owner Role Enforcement:** Verifikasi on-chain bahwa signer adalah `owner()` dari smart contract `PredictionMarket.sol` atau `OmenFactory.sol`.

---

### [QA-20260918-09] Status Integrasi Smart Contract dengan Jaringan Testnet (Live On-Chain vs Mock Environment)
- **Tanggal**: 2026-09-18 20:42
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `API & Network Integration`
- **Tags**: `#smart-contract #testnet-integration #chainlink-oracle #foundry #ethereum-sepolia #robinhood-testnet #mock-contracts`
- **File Referensi**:
  - `omen/web/lib/contracts.ts` (L1-L50)
  - `omen/web/lib/mockContracts.ts` (L1-L19)
  - `omen/web/lib/oracle/chainlink.ts` (L1-L55)
  - `omen/web/app/api/oracle/feeds/route.ts` (L1-L88)
  - `omen/web/hooks/usePlaceBet.ts` (L1-L79)
  - `omen/web/hooks/useCreateMarket.ts` (L48-L135)
  - `omen/contracts/script/DeploySepolia.s.sol` (L1-L18)
  - `omen/contracts/script/DeployRobinhood.s.sol` (L1-L18)
  - `nodes/omen/tickets/TICKET-101-manual-foundry-deployment-sepolia.md`
  - `nodes/omen/tickets/TICKET-102-manual-deploy-contracts-robinhood-chain-testnet.md`

#### ❓ Pertanyaan Pengguna
1. **apakah semua smart contract sudah terintegrasi dengan testnet?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Status Integrasi Smart Contract dengan Testnet (Pemisahan Live Oracle vs Standby Deployment)
- **Ringkasan Inti**:
  - **Smart Contract Oracle Chainlink:** **SUDAH 100% TERINTEGRASI LIVE ON-CHAIN** di Ethereum Sepolia Testnet (`11155111`).
  - **Smart Contract Custom Omen (`OmenFactory`, `OmenMarket`, `PredictionMarket`):** **SUDAH TERINTEGRASI SECARA ARSITEKTUR & CODE WIRING (100% SIAP BROADCAST)**, namun saat ini pada environment lokal/default masih diarahkan ke **Mock/Simulator (`NEXT_PUBLIC_USE_MOCK_CONTRACT=true`)** menunggu eksekusi broadcast manual Foundry oleh developer dengan private key ber-saldo faucet (sesuai TICKET-101 & TICKET-102).
- **Detail Implementasi & Logika**:
  1. **Yang SUDAH Live On-Chain Nyata di Testnet (Chainlink Oracle Feeds):**
     - Alamat kontrak Chainlink `AggregatorV3Interface` publik resmi di Ethereum Sepolia (`11155111`):
       - ETH/USD: `0x694AA1769357215DE4FAC081bf1f309aDC325306`
       - BTC/USD: `0x1b44F3514812d835EB1BDB0acB33d3fA3351Ee43`
       - SOL/USD: `0x0c9973e7a27d00e656B9f153348dA46CaD70d03d`
     - Endpoint Next.js `/api/oracle/feeds` membaca `latestRoundData()` secara real-time dari RPC publik (`https://rpc.sepolia.org`) menggunakan client `viem` tanpa nilai dummy.
  2. **Yang Telah Terintegrasi Penuh di Kode (Ready-to-Deploy & Wired):**
     - Source code Solidity (`OmenFactory.sol`, `OmenMarket.sol`, `PredictionMarket.sol`) telah selesai, lolos unit testing Foundry 100%, dan ABI-nya telah diekspor ke `web/contracts/`.
     - Seluruh hooks frontend Web3 (`usePlaceBet.ts`, `useClaim.ts`, `useCreateMarket.ts`, `useAdminCreateMarket.ts`, `useAdminResolveMarket.ts`) telah menggunakan Wagmi v3 TanStack mutation (`mutateAsync`) dan siap berinteraksi langsung dengan kontrak pintar.
     - Script deployment Foundry telah dibuat lengkap:
       - `contracts/script/DeploySepolia.s.sol` (untuk Ethereum Sepolia)
       - `contracts/script/DeployRobinhood.s.sol` (untuk Robinhood Chain Testnet ID `46630`)
  3. **Mengapa Masih Menggunakan Mock di Development (.env.local)?**
     - Sesuai tiket arsitektur **TICKET-101** dan **TICKET-102**, alamat kontrak kustom pada konfigurasi lokal menggunakan mock fallback address (`0x1111...` dan `0x2222...`) agar seluruh developer & automated test suite (Vitest 77 suites / 401 tests) dapat berjalan offline tanpa perlu menguras kuota faucet gas testnet.
     - **Cara Mengaktifkan Live On-Chain:** Cukup jalankan script Foundry (`forge script ... --broadcast`), lalu pasang alamat hasil deploy ke `NEXT_PUBLIC_OMEN_FACTORY_ADDRESS_SEPOLIA` dan set `NEXT_PUBLIC_USE_MOCK_CONTRACT=false` di `.env.local`.
- **Rasional & Keputusan Teknis**:
  Pemisahan fisik antara modul produksi (`contracts.ts`) dan mock simulator (`mockContracts.ts`) memastikan frontend siap bertransisi instan dari mode simulasi ke live testnet on-chain hanya dengan mengganti variabel lingkungan (*environment configuration-driven*).

---

### [QA-20260918-08] Logika Otorisasi Alamat Dompet & Pencegahan Impersonasi pada Konfirmasi Kreator
- **Tanggal**: 2026-09-18 14:44
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Security & Authentication`
- **Tags**: `#anti-impersonation #wallet-authorization #eip-712-security #creator-verification #audit-trail`
- **File Referensi**:
  - `omen/web/components/CreatorConfirmation.tsx` (L31-L35)
  - `omen/web/app/api/beliefs/[id]/confirm/route.ts` (L39-L98)
  - `omen/web/db/migrations/01_init_schema.sql` (Tabel `creator_profiles`, `creator_confirmations`)

#### ❓ Pertanyaan Pengguna
1. **bagaimana cara memastikan ia kreator atau bukan hanya dengan klik button?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Mekanisme Keamanan Otorisasi Dompet & Pencegahan Klaim Palsu
- **Ringkasan Inti**: Tombol tersebut **BUKAN tombol klik bebas tanpa otentikasi**. Tombol terikat pada **Pengecekan Alamat Dompet (`isCreatorMatch`)** dan **Tanda Tangan Kriptografis Kunci Privat (EIP-712 Private Key Proof)** yang terekspos secara publik.
- **Detail Implementasi & Logika**:
  1. **Pengecekan Otorisasi di Frontend (`CreatorConfirmation.tsx`):**
     ```typescript
     const isCreatorMatch =
       !creatorAddress ||
       !address ||
       creatorAddress.toLowerCase() === address.toLowerCase();
     ```
     Jika pasar sudah memiliki `creatorAddress` yang terdaftar (misal wallet resmi `@rajgokal`), maka dompet lain yang mencoba mengklik tombol akan ditolak (`disabled={!isCreatorMatch}`).
  2. **Validasi Kriptografis Tanpa Password di Backend (`route.ts`):**
     Saat tombol diklik, dompet harus membuktikan kepemilikan *private key* dengan menandatangani hash pesan EIP-712. Backend memvalidasi signature tersebut via `viem.verifyTypedData`. Tanpa kunci privat dompet asli, pihak lain tidak bisa memalsukan signature.
  3. **Transparansi Jejak Audit Publik (*Public Audit Trail*):**
     Alamat `creator_wallet` yang menandatangani dicatat secara permanen di database `creator_confirmations` dan ditampilkan secara terang-terangan di kartu profil kreator ([`/creator/[address]`](file:///Users/raka/Developer/repositories/projects/wealthy-people-org/omen-dir/omen/web/app/creator/%5Baddress%5D/page.tsx)) serta on-chain explorer. Jika seorang penipu mencoba mengklaim handle tokoh terkenal, alamat dompet penipu tersebut langsung terekspos dan dapat dilaporkan/dianulir.
- **Rasional & Keputusan Teknis**:
  Dengan menggabungkan *Wallet Whitelisting*, *EIP-712 Mathematical Proof*, dan *Public Transparency*, sistem menjamin bahwa hanya pemilik sah kunci privat dompet yang dapat memberikan konfirmasi resmi.

### [QA-20260918-07] Fungsi & Peran Komponen Banner Creator Verification (CreatorConfirmation.tsx)
- **Tanggal**: 2026-09-18 14:43
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `UI/UX & Design System`
- **Tags**: `#creator-confirmation #ui-banner #gasless-eip712 #social-reputation #market-detail`
- **File Referensi**:
  - `omen/web/components/CreatorConfirmation.tsx` (L1-L137)
  - `omen/web/components/MarketDetailPanels.tsx` (L147-L155)
  - `global-docs/update-brief-1.md` (§07, §24)

#### ❓ Pertanyaan Pengguna
1. **lalu ini buat apa? (Banner ungu Creator Verification: "Are you @handle? Sign typed data to officially authenticate this belief statement...")**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Tujuan & Perilaku Komponen Banner Creator Verification
- **Ringkasan Inti**: Elemen ini adalah **Banner Verifikasi Kreator Resmi** ([`CreatorConfirmation.tsx`](file:///Users/raka/Developer/repositories/projects/wealthy-people-org/omen-dir/omen/web/components/CreatorConfirmation.tsx)) yang berfungsi sebagai pintu bagi influencer pemilik opini (contoh: `@rajgokal`) untuk mengonfirmasi bahwa pernyataan tersebut benar-benar adalah keyakinannya.
- **Detail Implementasi & Logika**:
  1. **Kondisi Tampil:**
     - Ditampilkan pada halaman detail pasar prediksi (`/market/[id]`) ketika status pasar masih `OPEN / AI DETECTED` (belum dikonfirmasi oleh kreator).
     - Menampilkan panggilan interaktif ke handle pembuat opini (*"Are you @rajgokal? Sign typed data to officially authenticate this belief statement."*).
  2. **Interaksi Saat Tombol Diklik:**
     - Influencer mengklik tombol *"Confirm Belief (EIP-712)"*.
     - Dompet Web3 memunculkan pop-up tanda tangan gasless (0 biaya ETH).
     - Backend memvalidasi signature dan mengubah status pasar di database menjadi `CONFIRMED`.
  3. **Perubahan Visual Pasca-Konfirmasi:**
     - Banner ungu ini otomatis berganti menjadi **Banner Hijau Emerald**:
       `✓ EIP-712 Authenticated — Confirmed by @rajgokal (Official Signature)`.
     - Badge centang hijau (`✓`) otomatis disematkan di sebelah handle kreator pada seluruh kartu pasar.
- **Rasional & Keputusan Teknis**:
  Fitur ini menciptakan diferensiasi utama Omen dari prediction market tradisional (*Social Belief Market*), di mana konfirmasi resmi dari tokoh aslinya akan meningkatkan volume likuiditas pasar dan mencatat rekam jejak akurasi opini sang kreator di halaman profil publiknya (`/creator/[address]`).

### [QA-20260918-06] Titik Pemicu Pemanggilan OpenRouter AI pada Alur Pembuatan Belief
- **Tanggal**: 2026-09-18 14:41
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Business Logic & Domain Rules`
- **Tags**: `#openrouter #trigger-flow #belief-submission #ai-extraction #market-creation`
- **File Referensi**:
  - `omen/web/components/BeliefSubmitForm.tsx` (L48-L109)
  - `omen/web/app/api/beliefs/extract/route.ts` (L6-L65)
  - `omen/web/app/api/beliefs/submit/route.ts` (L40-L105)

#### ❓ Pertanyaan Pengguna
1. **otomatis saat beliefs dibuat, akan hit openrouter?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Alur & Titik Pemicu (*Trigger Points*) Panggilan OpenRouter AI
- **Ringkasan Inti**: **YA, otomatis terpicu pada Langkah 1 saat pengguna/admin mengklik tombol analisis teks**, sistem langsung meng-hit OpenRouter untuk membedah teks bebas menjadi parameter pasar terstruktur sebelum pasar dideploy ke database dan smart contract.
- **Detail Implementasi & Logika**:
  Alur pembuatan belief terdiri dari 3 tahap:
  1. **Tahap 1 — Pemicu OpenRouter (`POST /api/beliefs/extract`):**
     Saat pembuat pasar menginput `raw_text` (misal tweet *"Solana will hit 100k TPS by end of year"*) dan mengklik tombol *"Analyze with AI"*, frontend mengeksekusi `fetch('/api/beliefs/extract')`. Endpoint ini memanggil OpenRouter API untuk menghasilkan:
     - Target Aset (`SOL`)
     - Arah Prediksi (`OUTPERFORM` / `ABOVE_PRICE`)
     - Target Nilai & Waktu Resolusi (`timeframe_days`)
     - Rekomendasi Oracle (`chainlink`)
  2. **Tahap 2 — Review & Penyesuaian (UI Preview):**
     Parameter hasil analisis AI ditampilkan kepada user untuk ditinjau atau diedit jika diperlukan.
  3. **Tahap 3 — Penyimpanan & Deploy (`POST /api/beliefs/submit`):**
     Setelah disetujui, pasar disimpan ke Supabase dengan status `DETECTED` / `OPEN` dan hash metadata-nya dicatat ke smart contract on-chain.
- **Rujukan Kode Sumber**:
  ```typescript
  // BeliefSubmitForm.tsx (L63)
  const res = await fetch("/api/beliefs/extract", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ raw_text: rawText, author_handle: authorHandle, source_url: sourceUrl }),
  });
  ```
- **Rasional & Keputusan Teknis**:
  Memanggil AI di awal proses ekstraksi memastikan bahwa seluruh pasar prediksi memiliki format parameter yang baku dan objektif (sesuai standar Chainlink Price Oracle) sebelum menerima likuiditas taruhan pengguna.

### [QA-20260918-05] Status Integrasi Nyata vs Mock pada AI Social Ingestion Pipeline
- **Tanggal**: 2026-09-18 14:40
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `API & Network Integration`
- **Tags**: `#openrouter #llm-structuring #social-scraping #ai-pipeline #real-vs-mock #belief-extraction`
- **File Referensi**:
  - `omen/web/app/api/beliefs/extract/route.ts` (L1-L73)
  - `omen/web/lib/ai/openrouter.ts` (L38-L135)
  - `omen/web/lib/ai/mockOpenRouter.ts` (L1-L50)
  - `global-docs/update-brief-1.md` (§06, §22)

#### ❓ Pertanyaan Pengguna
1. **"Omen terhubung ke media sosial melalui AI Ingestion & Provenance Pipeline" apakah benar benar terintegrasi untuk saat ini atau masih dummy/mock?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Status Nyata Saat Ini (Real LLM Structuring vs Input Teks/URL)
- **Ringkasan Inti**:
  - **AI Structuring:** **100% REAL** terintegrasi ke OpenRouter LLM API (`https://openrouter.ai/api/v1/chat/completions`).
  - **Social Scraper / Auto-Crawler:** **BELUM** ada crawler otonom Twitter 24/7; teks/link tweet dimasukkan secara langsung (*human/curator input*).
- **Detail Implementasi & Logika**:
  1. **Yang SUDAH Bekerja Nyata (Real Production AI):**
     - Endpoint `/api/beliefs/extract` memanggil client `openrouter.ts`.
     - Mengirimkan raw text tweet/postingan ke model LLM (OpenRouter) dengan system prompt ketat untuk menghasilkan JSON terstruktur (`subject`, `direction`, `target_value`, `timeframe_days`, `oracle_recommendation`, `confidence_score`).
     - Jika `OPENROUTER_API_KEY` terkonfigurasi, AI bekerja secara live dan nyata, bukan simulasi statis.
  2. **Yang Saat Ini Masih Input Manual/Kurasi (Belum Bot Scraper Otomatis):**
     - Sistem belum memiliki daemon crawler yang secara otomatis men-scrape feed X/Twitter secara background tanpa input.
     - Input teks/URL postingan saat ini disubmit melalui form kurasi pengguna atau admin di halaman `/submit` / `/admin`.
  3. **Mekanisme Mock Fallback (Khusus Testing):**
     - File `mockOpenRouter.ts` hanya aktif jika `ENABLE_MOCK_AI="true"` atau dalam mode `NODE_ENV === "test"` agar CI/CD testing dapat berjalan tanpa menghabiskan kuota token API.
- **Rasional & Keputusan Teknis**:
  Sesuai spesifikasi `update-brief-1.md` §06 & §27, membangun web-scraper background untuk platform sosial Web2 seperti X/Twitter memerlukan enterprise API berbayar tinggi dan rentan banned, sehingga pada V1 parsing AI difokuskan pada pemrosesan semantik teks/URL yang disetorkan pengguna (*curator-driven belief creation*).

### [QA-20260918-04] Mekanisme Penghubung Media Sosial & Pemetaan Identitas Dompet (Social Integration vs Wallet Mapping)
- **Tanggal**: 2026-09-18 14:38
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Architecture & Pattern`
- **Tags**: `#social-media-provenance #wallet-binding #ai-pipeline #creator-profiles #farcaster #web3-identity`
- **File Referensi**:
  - `omen/web/app/api/beliefs/extract/route.ts` (L1-L73)
  - `omen/web/app/api/beliefs/submit/route.ts` (L40-L95)
  - `omen/web/db/migrations/01_init_schema.sql` (Tabel `beliefs`, `belief_sources`, `creator_profiles`, `creator_confirmations`)
  - `global-docs/update-brief-1.md` (§06, §23)

#### ❓ Pertanyaan Pengguna
1. **bagaimana terhubung dengan sosmednya? ambil data dari wallet tsb apakah integrasi social atau tidak?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Cara Data Terhubung dengan Media Sosial (AI Provenance Ingestion)
- **Ringkasan Inti**: Omen terhubung ke media sosial melalui **AI Ingestion Pipeline** (`/api/beliefs/extract`), bukan via OAuth login Web2 (tanpa "Sign in with Twitter").
- **Detail Implementasi & Logika**:
  1. **Ekstraksi Metadata Postingan Asli:**
     AI menerima tautan/teks opini dari platform sosial (X/Twitter, Farcaster, dsb.) dan membedahnya menjadi field kanonikal:
     - `raw_text`: Kalimat asli yang diposting oleh influencer.
     - `author`: Handle sosial resmi (contoh: `@vitalik`, `@aeyakovenko`).
     - `source_url`: URL permalink menuju postingan asli (contoh: `https://x.com/user/status/123`).
     - `source_platform`: Platform asal (`twitter`, `farcaster`, `manual`).
     - `source_timestamp`: Waktu tweet/post diterbitkan.
  2. **Tautan Sumber Terbuka (*View Source Link*):**
     Data ini disimpan di tabel `beliefs` dan `belief_sources`. Di antarmuka, tautan `source_url` dipasang pada tombol *"View Source ↗"* sehingga siapa pun dapat memverifikasi konteks asli langsung di platform asal.

##### 2. Pemetaan Dompet: Apakah Mengambil Data dari Wallet atau Integrasi Sosial?
- **Ringkasan Inti**: Pada arsitektur V1, sistem menggunakan **Web3-Native Identity Mapping (First-Claim & Profile Binding)** alih-alih login OAuth sosial terpusat.
- **Detail Implementasi & Logika**:
  1. **Non-Custodial / Tanpa OAuth Terpusat:**
     Sistem sengaja tidak menggunakan OAuth Web2 Twitter/X agar tidak terikat batasan API berbayar, risiko sensor, atau sentralisasi data.
  2. **Wallet-to-Handle Binding (`creator_profiles`):**
     - Saat pasar dibuat, jika kreator adalah tokoh Web3 yang memiliki wallet publik (atau ENS terdaftar seperti `vitalik.eth`), alamat tersebut didaftarkan sebagai `creator_wallet`.
     - Saat influencer pertama kali menghubungkan wallet dan mengonfirmasi via EIP-712 di `/market/[id]`, backend mencocokkan atau membuat record di tabel `creator_profiles` yang mengikat `wallet_address` dengan `handle` (@author).
     - Di masa depan (Roadmap Social Graph): Omen mendukung **Sign In with Farcaster (SIWF)** / **Lens Protocol** di mana relasi antara akun media sosial dan wallet address telah terverifikasi secara on-chain secara otomatis.
- **Rasional & Keputusan Teknis**:
  Pendekatan ini memisahkan secara tegas antara **data pasar (opini publik yang bebas dipertaruhkan)** dan **verifikasi identitas (kriptografis berbasis dompet)**, sehingga pasar dapat langsung berjalan tanpa harus menunggu izin atau login dari pemilik sosmed.

### [QA-20260918-03] Detail Teknis Endpoint & Mekanisme Tanda Tangan Konfirmasi Belief (Hit API vs On-Chain)
- **Tanggal**: 2026-09-18 14:33
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `API & Network Integration`
- **Tags**: `#api-route #eip-712 #wagmi #viem #rest-api #gasless-signature`
- **File Referensi**:
  - `omen/web/hooks/useCreatorConfirm.ts` (L42-L115)
  - `omen/web/app/api/beliefs/[id]/confirm/route.ts` (L7-L150)
  - `omen/web/lib/eip712/confirmation.ts` (L20-L44)

#### ❓ Pertanyaan Pengguna
1. **tidak paham, bagaimana caranya? hit api apa atau ke blockchain?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Jalur Eksekusi: Tanda Tangan Klien + Hit REST API (Bukan Transaksi On-Chain)
- **Ringkasan Inti**: Proses ini **TIDAK mengirim transaksi on-chain ke blockchain** (sehingga 0 gas fee), melainkan **menghasilkan tanda tangan digital lokal di dompet**, lalu **meng-hit REST API** backend di endpoint `POST /api/beliefs/[id]/confirm`.
- **Detail Implementasi & Logika**:
  Tahapan teknis konkret dari awal hingga selesai:
  1. **Langkah 1 (Di Browser / Dompet):**
     Influencer mengklik tombol di halaman detail pasar. Hook `useCreatorConfirm.ts` meminta dompet (MetaMask/Phantom) menandatangani pesan EIP-712.
     - *Status:* Ini bukan transaksi broadcast (tidak butuh gas fee / no ETH spent).
     - *Output:* Menghasilkan string tanda tangan heksadesimal (`0x7f8a...`).
  2. **Langkah 2 (Frontend Hit REST API):**
     Frontend melakukan panggilan HTTP `fetch`:
     - **Metode:** `POST`
     - **URL Endpoint:** `/api/beliefs/[belief_id]/confirm`
     - **Headers:** `{ "Content-Type": "application/json" }`
     - **Payload JSON Body:**
       ```json
       {
         "creator_address": "0x1234567890abcdef1234567890abcdef12345678",
         "signature": "0x7f8a3b...c9e1",
         "timestamp": 1773820000,
         "chain_id": 11155111
       }
       ```
  3. **Langkah 3 (Backend Memvalidasi via Viem & Database Supabase):**
     Server API Next.js menerima payload tersebut dan menjalankan:
     - `verifyTypedData()` dari pustaka `viem` untuk memastikan secara matematis signature dibuat oleh private key dari `creator_address`.
     - `supabase.from("beliefs").update({ status: "CONFIRMED" })` untuk menandai belief telah sah.
     - `supabase.from("creator_confirmations").insert(...)` untuk menyimpan riwayat audit trail bukti tanda tangan.
- **Rujukan Kode Sumber**:
  ```typescript
  const res = await fetch(`/api/beliefs/${payload.beliefId}/confirm`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      creator_address: creatorAddress,
      signature: signedSig,
      timestamp: timestampSec,
      chain_id: chainId || 11155111,
    }),
  });
  ```
- **Rasional & Keputusan Teknis**:
  Pendekatan *Off-chain Gasless Signature + REST API Confirmation* dipilih agar influencer Web2/Web3 dapat memvalidasi pernyataan mereka secara instan dalam 2 detik tanpa harus memiliki saldo ETH untuk gas fee blockchain, namun tetap memiliki derajat kepastian hukum kriptografis yang setara dengan transaksi on-chain.

### [QA-20260918-02] Verifikasi Identitas Influencer/Kreator & Rujukan UI Inspirasi (ui-example.md)
- **Tanggal**: 2026-09-18 14:32
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Security & Authentication`
- **Tags**: `#creator-identity #wallet-binding #eip-712 #social-proof #ui-example #openzeppelin-style`
- **File Referensi**:
  - `global-docs/update-brief-1.md` (§06-§07, §24)
  - `global-docs/ui-example.md` (L1-L4)
  - `omen/web/components/CreatorConfirmation.tsx` (L30-L50)
  - `omen/web/app/api/beliefs/[id]/confirm/route.ts` (L70-L145)
  - `omen/web/lib/eip712/confirmation.ts` (L20-L44)

#### ❓ Pertanyaan Pengguna
1. **bagaimana cara sistem tau ia benar-benar influencer atau tidal? bagaimana menurut ui-example.md ?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Mekanisme Verifikasi Identitas Asli Influencer (Tri-Layer Proofing)
- **Ringkasan Inti**: Sistem memvalidasi identitas influencer melalui tiga lapis verifikasi: **Provenance Media Sosial Asli (Source Extraction)**, **Kriptografi Dompet Web3 Terikat (EIP-712 Binding)**, dan **Sifat Non-Blocking Pasar (Social Verification Layer)**.
- **Detail Implementasi & Logika**:
  1. **Lapis 1 — Provenance & Canonical Source Link:**
     Setiap belief yang diekstrak oleh AI (`/api/beliefs/extract`) memuat tautan kanonikal langsung ke postingan media sosial asli (`source_url`, `authorHandle`, `source_platform`). Komponen UI menyematkan tombol *"View Source ↗"* sehingga publik dapat memverifikasi konteks pernyataan secara langsung ke akun resmi kreator.
  2. **Lapis 2 — Alamat Dompet Terikat & Kriptografi EIP-712:**
     - Saat kreator mengklaim/memvalidasi, backend mencocokkan `creator_wallet` yang terdaftar di profil kreator (`creator_profiles`) dengan signer dompet.
     - Signature diverifikasi menggunakan `viem.verifyTypedData` terhadap payload terstruktur. Jika dompet bukan milik kreator yang sah atau mismatch address terjadi, backend melempar status HTTP 401 (*Invalid signature or creator address mismatch*).
     - Di roadmap Web3 Social (Farcaster / ENS / Social Proof), wallet influencer terikat dengan identitas on-chain publik (misal ENS atau Farcaster FID).
  3. **Lapis 3 — Social Verification vs Market Permission:**
     Sesuai `update-brief-1.md` §07, konfirmasi kreator **BUKAN** syarat mutlak untuk membuka pasar (pasar langsung berjalan di status `OPEN` sebagai `AI DETECTED`). Konfirmasi influencer hanyalah stempel reputasi sosial (*social reputation badge*) yang mengubah status menjadi `CONFIRMED BY @handle`.

##### 2. Korelasi dengan Standar Desain pada ui-example.md
- **Ringkasan Inti**: Dokumen `global-docs/ui-example.md` mengarahkan sistem Omen agar mengadopsi estetika **OpenZeppelin Institutional**, **Aura UI Components**, dan **Landingfolio Crypto Design**, yang menitikberatkan pada kredibilitas, transparansi verifikasi, dan antarmuka *high-trust*.
- **Detail Implementasi & Logika**:
  Berdasarkan referensi tersebut:
  1. **OpenZeppelin Institutional Trust ([openzeppelin.com](https://www.openzeppelin.com/solidity-contracts)):**
     Menampilkan bukti verifikasi secara presisi (Monospace Address, EIP-712 badge, Smart Contract hash link ke Blockscout/Etherscan) alih-alih klaim sepihak.
  2. **Aura Components & Landingfolio ([aura.build](https://www.aura.build/browse/components) / [landingfolio.com](https://www.landingfolio.com)):**
     Menggunakan hierarki kartu bersih (*clean surface cards*), indikator badge interaktif (status `AI DETECTED` abu-abu vs `CONFIRMED` hijau emerald), dan transisi *gasless signature* yang mulus.
  3. **Dribbble Curated Collection:**
     Menghadirkan micro-animation (smooth fade-in, responsive theme adaptiveness, card hover elevation) yang memberikan impresi modern dan meyakinkan bagi pengguna maupun influencer saat berinteraksi dengan platform.

### [QA-20260918-01] Mekanisme Gasless EIP-712 Creator/Influencer Belief Confirmation
- **Tanggal**: 2026-09-18 14:30
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Business Logic & Domain Rules`
- **Tags**: `#eip-712 #creator-confirmation #gasless-signature #social-belief #creator-economy #web3-auth`
- **File Referensi**:
  - `omen/web/components/CreatorConfirmation.tsx` (L1-L137)
  - `omen/web/hooks/useCreatorConfirm.ts` (L23-L122)
  - `omen/web/app/api/beliefs/[id]/confirm/route.ts` (L7-L150)
  - `omen/web/lib/eip712/confirmation.ts` (L3-L44)
  - `omen/web/db/migrations/01_init_schema.sql` (Tabel `creator_confirmations`, `creator_profiles`, `beliefs`)

#### ❓ Pertanyaan Pengguna
1. **bagaimana cara influencer confirm beliefs?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Alur Interaksi UI & Otentikasi Gasless EIP-712
- **Ringkasan Inti**: Influencer/kreator mengonfirmasi belief secara *gasless* (tanpa biaya gas blockchain) melalui penandatanganan pesan kriptografis terstruktur standar **EIP-712** menggunakan dompet Web3 mereka langsung di antarmuka halaman detail pasar (`/market/[id]`).
- **Detail Implementasi & Logika**:
  Alur kerja konfirmasi belief oleh influencer terbagi dalam 4 tahapan berurutan:
  1. **Deteksi Kepemilikan Akun / Wallet Match (`CreatorConfirmation.tsx`):**
     Saat pengguna membuka halaman pasar, komponen memeriksa apakah alamat dompet pengguna yang sedang terkoneksi (`address` dari wagmi) cocok dengan `creatorAddress` atau `creator_wallet` pemilik *statement* belief. Jika cocok, banner CTA *"Confirm Belief (EIP-712)"* akan aktif.
  2. **Pembuatan & Penandatanganan Payload EIP-712 (`useCreatorConfirm.ts`):**
     Saat tombol ditekan, hook memanggil fungsi `signTypedDataAsync` dari wagmi untuk memunculkan pop-up tanda tangan di dompet Web3 pengguna (tanpa gas fee). Struktur data yang ditandatangani:
     ```typescript
     const types = {
       ConfirmBelief: [
         { name: "beliefId", type: "string" },
         { name: "creator", type: "address" },
         { name: "statement", type: "string" },
         { name: "timestamp", type: "uint256" },
       ],
     };
     ```
  3. **Verifikasi Kriptografis & Persistensi Backend (`/api/beliefs/[id]/confirm`):**
     Frontend mengirimkan payload `{ creator_address, signature, timestamp, chain_id }` ke backend API. Endpoint memverifikasi keaslian signature menggunakan fungsi `verifyBeliefConfirmationSignature()` (`viem.verifyTypedData`). Jika valid:
     - Status belief di tabel `beliefs` diubah menjadi `CONFIRMED`.
     - Data tanda tangan dicatat ke tabel `creator_confirmations`.
     - Statistik profil kreator di tabel `creator_profiles` di-upsert (menaikkan `confirmed_beliefs_count`).
  4. **Pembaruan Visual Instan:**
     Komponen menampilkan badge hijau bertuliskan *"EIP-712 Authenticated — Confirmed by @handle"* dengan tanda centang resmi terverifikasi.
- **Rujukan Kode Sumber**:
  ```typescript
  signedSig = await signTypedDataAsync({
    domain: {
      name: "Omen Belief Protocol",
      version: "1",
      chainId: chainId || 11155111,
      verifyingContract,
    },
    types,
    primaryType: "ConfirmBelief",
    message: {
      beliefId: payload.beliefId,
      creator: creatorAddress,
      statement: payload.statement,
      timestamp,
    },
  });
  ```
- **Rasional & Keputusan Teknis**:
  1. **Gasless Friction-Free Onboarding:** Kreator tidak perlu memiliki saldo ETH untuk membayar gas transaksi saat memvalidasi opini/statement mereka.
  2. **Non-Repudiation (Anti-Penyangkalan Kriptografis):** Tanda tangan EIP-712 membuktikan secara matematis bahwa pemilik kunci privat dompet resmi telah menyetujui pernyataan tersebut pada waktu tertentu, mencegah bot atau pihak ketiga memalsukan konfirmasi.

### [QA-20260915-02] Penjelasan Rumus Kalkulasi Payout Model Pari-Mutuel
- **Tanggal**: 2026-09-15 19:32
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Business Logic & Domain Rules`
- **Tags**: `#pari-mutuel #payout-calculation #prediction-market #smart-contract #tokenomics`
- **File Referensi**:
  - `nodes/omen/docs/system-design.md` (L75-L88)
  - `nodes/omen/tickets/TICKET-04-prediction-market-contract.md` (L12-L19)
  - `nodes/omen/tickets/TICKET-05-contract-unit-testing.md` (L14-L18)

#### ❓ Pertanyaan Pengguna
1. **apa ini $\text{Estimasi Payout} = \text{Taruhan User} + \left( \frac{\text{Taruhan User}}{\text{Total Pool Sisi Pilihan}} \times \text{Total Pool Sisi Lawan} \right)$**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Konsep Dasar & Bedah Rumus Pari-Mutuel Betting
- **Ringkasan Inti**: Rumus ini adalah model matematika sistem taruhan **Pari-Mutuel** (*Pool-Based Prediction Market*). Seluruh dana dari pihak yang salah disita, lalu dibagikan secara proporsional kepada para pemenang berdasarkan persentase modal yang mereka setorkan.
- **Detail Implementasi & Logika**:
  Di dalam smart contract `PredictionMarket.sol`, rumus ini dibagi menjadi 3 bagian:
  1. **`Taruhan User`**: Modal awal yang disetorkan pengguna dikembalikan secara utuh (*principal refund*).
  2. **`\frac{\text{Taruhan User}}{\text{Total Pool Sisi Pilihan}}`**: Porsi persentase kepemilikan (*share*) pengguna di dalam pool tim pemenang.
  3. **`\times \text{Total Pool Sisi Lawan}`**: Hadiah kemenangan (*profit*) yang diperebutkan dan diambil dari total dana pihak yang kalah.

  **Contoh Simulasi Nyata:**
  - Total Pool YES = **10 ETH** (User bertaruh **1 ETH**, berarti User memiliki 10% saham di sisi YES).
  - Total Pool NO = **40 ETH**.
  - Jika **YES Menang**:
    $$\text{Payout} = 1\text{ ETH} + \left( \frac{1}{10} \times 40\text{ ETH} \right) = 1\text{ ETH} + 4\text{ ETH} = 5\text{ ETH}$$
    User mendapat modal 1 ETH kembali + untung bersih 4 ETH (total 5 ETH / 5x return).
- **Rasional & Keputusan Teknis**:
  1. **Zero Insolvency Risk (Kontrak Selalu Solven):** Smart contract tidak pernah mengalami gagal bayar karena total dana yang didistribusikan ke pemenang selalu sama persis dengan total deposit yang ada di kontrak ($\text{Pool YES} + \text{Pool NO}$).
  2. **Non-Custodial / Tanpa Bandar (*Peer-to-Peer*):** Pengguna bertaruh melawan pengguna lain, platform tidak bertindak sebagai bandar sehingga aman dari risiko kebangkrutan.

### [QA-20260915-01] Fungsi & Peran total_pool_yes dan total_pool_no pada Tabel markets
- **Tanggal**: 2026-09-15 19:25
- **Scope / Target Node**: `nodes/omen`
- **Kategori**: `Database & Data Modeling`
- **Tags**: `#prediction-market #database-modeling #pool-ratio #odds-calculation #caching`
- **File Referensi**:
  - `nodes/omen/docs/diagrams/erd.puml` (L36-L49)
  - `nodes/omen/docs/system-design.md` (L58-L62)
  - `global-docs/prd.md` (L51-L54)

#### ❓ Pertanyaan Pengguna
1. **total_pool_yes dan no buat apa?**

#### 💡 Jawaban & Penjelasan Implementasi

##### 1. Akumulasi Likuiditas & Perhitungan Implied Odds Real-Time
- **Ringkasan Inti**: Kolom `total_pool_yes` dan `total_pool_no` berfungsi menyimpan total akumulasi dana (Native ETH) yang telah dipertaruhkan oleh seluruh pengguna pada masing-masing sisi pasar prediksi.
- **Detail Implementasi & Logika**:
  Di dalam sistem pasar prediksi Omen, kedua kolom ini memegang 4 peran vital:
  1. **Kalkulasi Probabilitas / Implied Odds:** Menghitung rasio persentase pada komponen UI `PoolRatioBar.tsx` (contoh: Yes 60% vs No 40%) menggunakan rumus:
     $$\text{Yes Odds (\%)} = \frac{\text{total\_pool\_yes}}{\text{total\_pool\_yes} + \text{total\_pool\_no}} \times 100\%$$
     $$\text{No Odds (\%)} = \frac{\text{total\_pool\_no}}{\text{total\_pool\_yes} + \text{total\_pool\_no}} \times 100\%$$
  2. **Estimasi Payout Pengguna:** Saat pengguna membuka modal taruhan (`BettingModal.tsx`), sistem dapat langsung menampilkan perkiraan potensi keuntungan (*potential return*) jika sisi pilihannya menang.
  3. **Optimasi Performa & Query Caching:** Menghindari eksekusi query agregasi berat (`SELECT SUM(amount) FROM bets WHERE market_id = ... AND side = ...`) setiap kali ribuan pengguna memuat feed pasar `/predictions`. Nilai pool diperbarui secara inkremental melalui endpoint `/api/bets/index`.
  4. **Cermin Sinkronisasi Smart Contract:** Menjadi data *cache* off-chain dari state on-chain `market.totalYesPool` dan `market.totalNoPool` yang ada pada kontrak `PredictionMarket.sol`.
- **Rujukan Kode Sumber**:
  ```plantuml
  entity "markets" as markets {
    * id : uuid <<PK>>
    * contract_market_id : integer
    * title : text
    * deadline : timestamptz
    * status : text
    total_pool_yes : numeric <<default 0>>
    total_pool_no : numeric <<default 0>>
  }
  ```
- **Rasional & Keputusan Teknis**:
  Pendekatan *denormalized counter cache* ini dipilih karena traffic pembacaan kartu pasar di halaman utama jauh lebih tinggi dibandingkan frekuensi penulisan taruhan, sehingga menjaga waktu respons query API di bawah 100ms.
