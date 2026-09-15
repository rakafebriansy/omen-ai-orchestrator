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
  - *(Belum ada entri)*
- **State Management & Data Flow**
  - *(Belum ada entri)*
- **Database & Data Modeling**
  - [[QA-20260915-01] Fungsi & Peran total_pool_yes dan total_pool_no pada Tabel markets](#qa-20260915-01-fungsi--peran-total_pool_yes-dan-total_pool_no-pada-tabel-markets)
- **API & Network Integration**
  - *(Belum ada entri)*
- **UI/UX & Design System**
  - *(Belum ada entri)*
- **Security & Authentication**
  - *(Belum ada entri)*
- **Testing & Quality Assurance**
  - *(Belum ada entri)*
- **Build, Tooling & DevOps**
  - *(Belum ada entri)*
- **Business Logic & Domain Rules**
  - [[QA-20260915-02] Penjelasan Rumus Kalkulasi Payout Model Pari-Mutuel](#qa-20260915-02-penjelasan-rumus-kalkulasi-payout-model-pari-mutuel)
- **Orchestrator & Workflow**
  - *(Belum ada entri)*

---

## 📚 Arsip Log Tanya-Jawab

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
