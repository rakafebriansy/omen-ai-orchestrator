---
id: TICKET-112
title: Redesign Admin Dashboard into Protocol Governance and Oracle Pipeline Monitor (V1 Alignment)
status: Done
priority: High
labels: [Frontend, Admin, Architecture, Refactor]
---

# Deskripsi
Berdasarkan dokumen arsitektur dan spesifikasi produk terbaru (`global-docs/update-brief-1.md`), fitur gamifikasi (Quests, Daily Check-in streak points, XP) telah sepenuhnya dihapus dari cakupan Omen V1 Social Belief Market. 

Halaman `/admin` saat ini masih memuat elemen *legacy* yang sudah usang, seperti tab "Manage Quests", form CRUD Quest, serta metrik "Configured Quests" dan "Gamification XP distribution rules". Selain itu, pada V1, pembuatan pasar dilakukan melalui pipeline *Social Belief Ingestion* (`/create` atau AI Ingestion) dan resolusi pasar dijalankan secara otomatis oleh **Chainlink Oracle Resolution Engine**, bukan melalui pembuatan/resolusi manual harian oleh admin.

Sesuai `update-brief-1.md` §09, §10, §19, §38, dan §45, peran Admin Dashboard pada Omen V1 difokuskan menjadi **Protocol Governance, Oracle & Price Feed Monitor, serta Emergency Circuit Breaker**.

## Usulan Arsitektur Baru Halaman `/admin` (V1):
1. **Overview Metrics Card (Header):**
   - **Total Active Markets:** Menampilkan jumlah pasar *Social Belief* yang sedang aktif di Sepolia & Robinhood Chain Testnet.
   - **Oracle Price Feeds Status:** Menampilkan status kesehatan feed Chainlink (ETH/USD, BTC/USD, SOL/USD) dan latensi snapshot.
   - **Emergency Alert / Circuit Breaker:** Indikator status protokol (Operational vs Paused).
2. **Tab 1: Social Beliefs & Market Pipeline Monitor (`beliefs-monitor`)**
   - Memantau alur status 6-tahap V1: `DETECTED` → `OPEN` → `CONFIRMED` (EIP-712 Verified) → `CLOSED` → `RESOLVED` → `SETTLED`.
   - Melihat rincian konsensus sosial (% AGREE vs DISAGREE) dan volume kapital on-chain.
3. **Tab 2: Chainlink Oracle Feeds & Auto-Resolution (`oracle-monitor`)**
   - Menampilkan harga spot terkini dari Chainlink Aggregator di testnet.
   - Daftar pasar yang mendekati deadline dan status trigger otomatis resolusi berdasarkan kondisi harga (Price Above, Price Below, Relative Performance).
4. **Tab 3: Emergency Controls & Manual Circuit Breaker (`emergency-controls`)**
   - Eksekusi prosedur darurat transparan: `Emergency Void / 100% Refund` (jika oracle feed gagal/rusak).
   - `Market Emergency Pause` (jika terdeteksi kerentanan kritis atau manipulasi pasar).
   - Log audit audit transparan untuk seluruh aksi privileged.
5. **Penghapusan Komponen Quest (Legacy Clean-up):**
   - Menghapus tab "Manage Quests", komponen `AdminQuestManagementForm.tsx`, dan ketergantungan API `/api/admin/quests` dari dashboard admin.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Hapus tab "Manage Quests" dan referensi `AdminQuestManagementForm` dari `web/app/admin/page.tsx`.
- [x] Perbarui 3 kartu metrik statistik pada header admin menjadi: *Active Social Belief Markets*, *Chainlink Price Feeds Status*, dan *Pending Automated Resolutions*.
- [x] Implementasikan tab *Social Beliefs Pipeline Monitor* yang menampilkan data pasar Supabase/on-chain dengan badge verifikasi EIP-712 creator.
- [x] Implementasikan tab *Oracle Feeds & Resolution Monitor* yang terhubung ke live Chainlink snapshot API (`/api/oracle/snapshot`).
- [x] Implementasikan tab *Emergency Governance Controls* untuk aksi `Emergency Void / Refund` dan `Protocol Pause` dengan konfirmasi keamanan berlapis.
- [x] Perbarui test suite Vitest agar memvalidasi struktur dashboard admin baru dengan kelulusan 100%.
- [x] Pastikan seluruh kode tetap mematuhi Zero-Comment Policy, validasi ESLint, dan typecheck TypeScript.

## Target Lingkup File (Affected Files)
- `web/app/admin/page.tsx`
- `web/components/AdminOracleMonitor.tsx`
- `web/components/AdminBeliefPipelineTable.tsx`
- `web/components/AdminEmergencyControls.tsx`
- `web/components/AdminMarketResolutionTable.tsx`
- `web/tests/admin-page.test.tsx`
- `web/tests/admin-oracle-monitor.test.tsx`
- `web/tests/admin-belief-pipeline.test.tsx`
- `web/tests/admin-emergency-controls.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Merancang dan mengimplementasikan komponen `AdminOracleMonitor.tsx` untuk memonitor feed data Chainlink (ETH/USD, BTC/USD, SOL/USD) dan trigger snapshot harga on-chain/database.
  2. Merancang dan mengimplementasikan komponen `AdminBeliefPipelineTable.tsx` untuk memantau siklus hidup pasar Social Beliefs 6-tahap V1 (`DETECTED`, `OPEN`, `CONFIRMED`, `CLOSED`, `RESOLVED`, `SETTLED`), skor AI confidence, konsensus kapital, dan validasi EIP-712.
  3. Merancang dan mengimplementasikan komponen `AdminEmergencyControls.tsx` untuk tata kelola darurat sirkuit pemutus (Protocol Pause/Resume, Emergency Market Void / 100% Refund, dan immutable audit log).
  4. Merefaktor `web/app/admin/page.tsx` untuk menghapus seluruh ketergantungan quest legacy dan menggantikannya dengan 5 tab V1 Protocol Governance modern.
  5. Menulis test suite komprehensif pada `admin-page.test.tsx`, `admin-oracle-monitor.test.tsx`, `admin-belief-pipeline.test.tsx`, dan `admin-emergency-controls.test.tsx`.
  6. Memvalidasi 100% kelulusan tes (77 test suites, 395 unit tests), 0 error TypeScript, dan 0 error ESLint dengan kepatuhan mutlak Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `web/app/admin/page.tsx`
  - `web/components/AdminOracleMonitor.tsx`
  - `web/components/AdminBeliefPipelineTable.tsx`
  - `web/components/AdminEmergencyControls.tsx`
  - `web/tests/admin-page.test.tsx`
  - `web/tests/admin-oracle-monitor.test.tsx`
  - `web/tests/admin-belief-pipeline.test.tsx`
  - `web/tests/admin-emergency-controls.test.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Menggantikan konsep CRUD Quest dengan Oracle Monitor & Emergency Circuit Breaker sesuai spesifikasi V1 pada update-brief-1.md.
