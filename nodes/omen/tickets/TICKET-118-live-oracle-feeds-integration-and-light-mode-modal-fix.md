---
id: TICKET-118
title: Live Oracle Feeds Integration and Light Mode Modal Backdrop Fix
status: Done
priority: High
labels: [Frontend, Backend, Oracle, Web3, BugFix]
---

# Deskripsi
Perbaikan styling overlay latar belakang modal/dialog pada Light Mode agar tidak menjadi hitam pekat (pitch black) dengan menerapkan kelas adaptif `bg-black/40 dark:bg-black/75 backdrop-blur-sm`. Selain itu, menghubungkan Oracle Pipeline & Live Feeds Monitor ke Smart Contract Chainlink on-chain secara langsung melalui endpoint baru `GET /api/oracle/feeds` dan `GET /api/oracle/snapshot`, serta membersihkan seluruh nilai dummy/hardcoded pada antarmuka.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Memperbarui overlay dialog/modal di seluruh 6 komponen modal agar tampil bersih dan transparan di Light Mode (`bg-black/40`) dan kontras di Dark Mode (`dark:bg-black/75`).
- [x] Membuat endpoint `GET /api/oracle/feeds` yang membaca `latestRoundData()` secara live dari kontrak Chainlink Sepolia via Viem RPC.
- [x] Menambahkan handler `GET /api/oracle/snapshot` untuk mengambil riwayat snapshot langsung dari Supabase.
- [x] Menyambungkan `AdminOracleMonitor.tsx` dengan `useEffect` dan auto-refresh on-chain tanpa simulasi acak.
- [x] Memvalidasi 77 test suites lulus 100% (398 unit tests) dan mematuhi Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/api/oracle/feeds/route.ts`
- `omen/web/app/api/oracle/snapshot/route.ts`
- `omen/web/components/AdminOracleMonitor.tsx`
- `omen/web/components/BettingModal.tsx`
- `omen/web/components/AdminMarketCreateForm.tsx`
- `omen/web/components/AdminMarketResolutionTable.tsx`
- `omen/web/components/AdminQuestManagementForm.tsx`
- `omen/web/components/NetworkSwitcherModal.tsx`
- `omen/web/components/AdminEmergencyControls.tsx`
- `omen/web/lib/oracle/chainlink.ts`
- `omen/web/types/api.ts`
- `omen/web/tests/admin-oracle-monitor.test.tsx`
- `omen/web/tests/api-oracle-snapshot.test.ts`

---

## AI Execution Log dan Output
- **Langkah Teknis Tereksekusi:**
  1. Memperbarui kelas backdrop modal pada `BettingModal.tsx`, `AdminMarketCreateForm.tsx`, `AdminMarketResolutionTable.tsx`, `AdminQuestManagementForm.tsx`, `NetworkSwitcherModal.tsx`, dan `AdminEmergencyControls.tsx` menjadi `bg-black/40 dark:bg-black/75 backdrop-blur-sm`.
  2. Mengimplementasikan `GET /api/oracle/feeds` di `web/app/api/oracle/feeds/route.ts` dengan eksekusi `fetchChainlinkPrice()` langsung ke Ethereum Sepolia AggregatorV3 contracts (ETH: `0x694AA176...`, BTC: `0x1b44F351...`).
  3. Mengimplementasikan `GET /api/oracle/snapshot` di `web/app/api/oracle/snapshot/route.ts` untuk query log snapshot Supabase terurut descending.
  4. Merefaktor `AdminOracleMonitor.tsx` untuk melakukan fetch live feeds dan live snapshots secara deterministik saat mount dan tombol refresh diklik.
  5. Menambahkan unit tests dan memvalidasi kelulusan 77 test suites (398 unit tests) dengan kepatuhan 100% Zero-Comment Policy.
- **Ringkasan File Terpengaruh:**
  - `web/app/api/oracle/feeds/route.ts` (NEW)
  - `web/app/api/oracle/snapshot/route.ts` (MODIFIED)
  - `web/components/AdminOracleMonitor.tsx` (MODIFIED)
  - `web/components/BettingModal.tsx` (MODIFIED)
  - `web/components/AdminMarketCreateForm.tsx` (MODIFIED)
  - `web/components/AdminMarketResolutionTable.tsx` (MODIFIED)
  - `web/components/AdminQuestManagementForm.tsx` (MODIFIED)
  - `web/components/NetworkSwitcherModal.tsx` (MODIFIED)
  - `web/components/AdminEmergencyControls.tsx` (MODIFIED)
  - `web/lib/oracle/chainlink.ts` (MODIFIED)
  - `web/types/api.ts` (MODIFIED)
  - `web/tests/admin-oracle-monitor.test.tsx` (MODIFIED)
  - `web/tests/api-oracle-snapshot.test.ts` (MODIFIED)
- **Catatan dan Keputusan Arsitektural:**
  - Pemanggilan on-chain Sepolia membaca data live harga Bitcoin $76,935.85 dan Ethereum $2,454.54 secara real-time via Viem RPC public client.
