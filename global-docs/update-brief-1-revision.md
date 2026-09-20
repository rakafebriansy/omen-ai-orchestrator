## Judul Issue
Activity Feed — Modal "On-Chain Transaction Receipt" (Decoded) + Ganti Seluruh Emoji Jadi Icon Set Konsisten

---

## Bagian A — Modal Detail Transaksi On-Chain

### Kondisi Saat Ini
`components/ActivityFeed.tsx` sudah menampilkan feed aktivitas publik (wallet, action AGREE/DISAGREE/CLAIM/RESOLVE, market, jumlah ETH, waktu) — ini sudah sesuai brief §35. Tapi tombol transaksi saat ini cuma link keluar polos ke block explorer (`getExplorerUrl()` → buka tab baru ke Etherscan/Blockscout). Belum ada tampilan detail transaksi di dalam aplikasi, dan chain dari tiap aktivitas juga tidak ditampilkan eksplisit ke user (cuma dipakai diam-diam buat nentuin URL explorer).

### Perubahan yang Diminta

**1. Tampilkan Chain Secara Eksplisit di Tiap Item Activity**
Omen berjalan di 2 chain (dual-testnet, §13): **Ethereum Sepolia** (`11155111`) dan **Robinhood Chain Testnet** (`46630`). Interface `ActivityItem` sudah punya field `chainId?: number` — tinggal dipakai buat nampilin badge nama chain di tiap baris feed, bukan cuma dipakai diam-diam buat generate link.

Tambahkan badge kecil di tiap item, contoh:
```
● Ethereum Sepolia     (chainId 11155111)
● Robinhood Chain      (chainId 46630)
```
Ini penting karena user perlu tahu di jaringan mana suatu posisi/klaim terjadi, terutama karena wallet yang sama bisa aktif di kedua testnet.

**2. Ganti Link Explorer Polos Jadi Modal "On-Chain Transaction Receipt"**
Saat user klik tombol transaksi, buka modal di dalam aplikasi (bukan langsung lompat ke tab baru) yang berisi:

- **Header**: Chain name + Chain ID + status (`Confirmed`), sama seperti badge di poin 1.
- **Transaction Hash**: full hash + tombol copy.
- **Decoded Function Call**: pakai `viem`'s `decodeFunctionData()` dengan ABI yang sudah ada di `web/contracts/OmenMarket.json` / `OmenFactory.json` / `PredictionMarket.json` — tampilkan nama function dan tiap parameter-nya apa adanya (contoh: `placeBet(bytes32 marketId, bool isAgree, uint256 amount)` beserta value tiap parameter).
- **Ringkasan posisi** (kalau actionnya AGREE/DISAGREE): Staked Value (ETH), Pool Share saat ini (%), posisi (AGREE/DISAGREE) — ini bisa dihitung dari data yang sudah ada di market (§05 Consensus vs Capital), tinggal ditarik ke level per-transaksi.
- **Detail block**: Block Number, Gas Price/Used, Execution Fee.
- **From / Interacted With**: address trader, address contract yang dipanggil (nama contract-nya juga ditampilkan, misal `OmenMarket`).
- **Link sekunder**: tetap sediakan link "View on Explorer ↗" di dalam modal — cuma dipindah jadi opsi tambahan, bukan satu-satunya cara lihat detail.

**3. Contoh Implementasi Decode**
```ts
import { decodeFunctionData } from "viem";
import OmenMarketAbi from "@/contracts/OmenMarket.json";

const { functionName, args } = decodeFunctionData({
  abi: OmenMarketAbi.abi,
  data: tx.input, // raw calldata dari tx
});
```
Ambil `tx` (termasuk `input`, `blockNumber`, `gasPrice`, `gasUsed`, `from`, `to`) dari RPC provider yang sesuai `chainId` item tersebut (Sepolia RPC atau Robinhood Chain RPC — pilih berdasarkan `item.chainId`, jangan hardcode ke satu chain saja).

### Definition of Done — Bagian A
- [ ] Tiap item di Activity Feed menampilkan badge nama chain (Ethereum Sepolia / Robinhood Chain Testnet) secara eksplisit, bukan cuma dipakai diam-diam di balik layar.
- [ ] Klik tombol transaksi membuka modal in-app (bukan langsung ke tab baru).
- [ ] Modal menampilkan calldata yang sudah di-decode (nama function + parameter), bukan cuma hash mentah.
- [ ] Modal tetap menyediakan link sekunder ke block explorer asli sesuai chain-nya masing-masing.
- [ ] Modal berfungsi dengan benar untuk transaksi dari KEDUA chain (Sepolia dan Robinhood Chain Testnet) — RPC yang dipanggil harus sesuai `chainId` item, tidak boleh hardcode satu chain saja.

---

## Bagian B — Ganti Seluruh Emoji Jadi Icon Set Konsisten (Lucide)

### Temuan
UI Omen saat ini pakai karakter emoji langsung sebagai icon di banyak komponen (⚡🔥🐸🏁🌐🏆📊🥇🥈🥉🎉🚀✨⚖⚠🛡). Ini bikin tampilan terasa generic/"AI slop" — beda-beda gaya render tiap OS/browser (emoji Apple vs Windows vs Android terlihat beda), dan gak sejalan sama arah visual "professional startup" yang sudah ditetapkan di 4 project lain.

Penyebabnya: **belum ada icon library ter-install** di project ini (`lucide-react`/sejenisnya gak ada di `package.json`). Emoji dipakai sebagai jalan pintas — termasuk modal di Bagian A nanti sebaiknya langsung pakai icon set ini dari awal, jangan sampai nambah emoji baru lagi.

### Solusi
Install **`lucide-react`** (ringan, tree-shakeable, dan konsisten dengan `shadcn/ui` yang sudah dipakai project ini per brief §22). Ganti seluruh emoji jadi komponen icon SVG.

```bash
npm install lucide-react
```

### Daftar Lengkap Penggantian

| Emoji | Lokasi (file) | Konteks Pemakaian | Ganti Jadi |
|---|---|---|---|
| ✨ | `app/admin/page.tsx`, `components/ActivityFeed.tsx` | Badge "MARKET CREATED" | `<Sparkles />` atau `<CirclePlus />` |
| 🏆 | `components/ActivityFeed.tsx`, `MarketCard.tsx`, `UserBetsTable.tsx` | Badge "PAYOUT CLAIM" / status "Won" | `<Trophy />` |
| ⚖ | `components/ActivityFeed.tsx` | Badge "RESOLUTION" | `<Scale />` |
| ⚡ | `AdminLoginForm.tsx`, `AdminOracleMonitor.tsx`, `MarketCategoryFilter.tsx`, `FeaturePillars.tsx`, `LiveActivityExplorer.tsx`, `SignalGapVisualizer.tsx` | Kategori "Crypto"/indikator live/cepat | `<Zap />` |
| ⚠ | `AdminEmergencyControls.tsx`, `AdminOracleMonitor.tsx` | Peringatan/warning admin | `<AlertTriangle />` |
| 🛡 | `AdminEmergencyControls.tsx` | Ikon proteksi/emergency guard | `<Shield />` |
| 🚀 | `BeliefSubmitForm.tsx` | Tombol "Deploy/Launch Market" | `<Rocket />` |
| 🎉 | `DailyCheckinWidget.tsx` | Notifikasi sukses check-in | `<PartyPopper />` atau `<CheckCircle2 />` (lebih restrained) |
| 📊 | `UserBetsTable.tsx` | Ikon statistik | `<BarChart3 />` |
| 🔥 | `MarketCategoryFilter.tsx`, `FeaturePillars.tsx`, `QuestsTeaser.tsx` | Kategori "Trending/Hot" | `<Flame />` |
| 🌐 | `MarketCategoryFilter.tsx` | Kategori "All/Macro" | `<Globe />` |
| 🏁 | `MarketCategoryFilter.tsx` | Kategori "Ending Soon" | `<Flag />` |
| 🐸 | `MarketCategoryFilter.tsx` | Kategori "Meme" | **Jangan pakai icon hewan literal** — ganti jadi tag warna/label teks polos per kategori (konsisten sama prinsip "no mascot/karakter" yang sudah dipakai di 4 project lain), atau custom icon abstrak kalau memang perlu visual pembeda |
| 🥇🥈🥉 | `LeaderboardTable.tsx` | Ranking top-3 leaderboard | Ganti jadi badge angka (`#1`/`#2`/`#3`) dengan warna berbeda (emas/perak/perunggu sebagai warna badge, bukan emoji medali) — lebih konsisten sama gaya data-terminal yang dipakai Omen |
| ✓ / ✕ | Banyak file (`BeliefCard`, `CreatorCard`, `MarketDetailPanels`, dll — 15+ lokasi) | Indikator centang/silang | `<Check />` / `<X />` — opsional tapi disarankan diseragamkan juga, karena render simbol Unicode ini juga sedikit beda-beda antar font/OS |
| ↗ / → / ← | Beberapa file landing | Panah navigasi/link keluar | `<ArrowUpRight />` / `<ArrowRight />` / `<ArrowLeft />` — opsional, prioritas rendah dibanding daftar di atas |

### Prioritas Pengerjaan
1. **Wajib**: seluruh emoji berwarna dekoratif (⚡🔥🐸🏁🌐🏆📊🥇🥈🥉🎉🚀✨⚖⚠🛡) — ini yang paling kentara efeknya ke kesan "AI slop".
2. **Opsional/nice-to-have**: seragamkan ✓/✕/panah jadi icon SVG juga, kalau waktu memungkinkan — dampaknya lebih kecil tapi tetap menambah konsistensi visual keseluruhan.

### Definition of Done — Bagian B
- [ ] `lucide-react` ter-install.
- [ ] Semua emoji dekoratif (kategori "wajib" di atas) sudah diganti jadi komponen icon dari lucide, ukuran & warna konsisten (ikutin token warna project, jangan warna default emoji).
- [ ] Kategori filter market (🐸 khususnya) tidak lagi pakai icon hewan literal — pakai label/warna atau icon abstrak.
- [ ] Leaderboard top-3 pakai badge angka berwarna, bukan emoji medali.
- [ ] Dicek tampilannya konsisten di berbagai browser (icon SVG gak akan berubah-ubah bentuk seperti emoji antar-OS).
- [ ] Modal "On-Chain Transaction Receipt" dari Bagian A dipastikan dari awal pakai icon Lucide, bukan emoji baru.

## Referensi
Pola modal transaksi di Bagian A terinspirasi dari referensi UI yang mengedepankan transparansi on-chain (decoded calldata + staking telemetry ditampilkan langsung di dalam app) — bukan untuk ditiru persis, hanya sebagai bahan perbandingan pola informasi yang ditampilkan.

---

## Bagian C — Seed Data Activity Harus Transaksi Asli di Testnet (Bukan Insert DB Biasa)

### Kenapa Ini Beda dari Seed Data Biasa
Modal di Bagian A membaca `tx.input` langsung dari RPC untuk di-decode. Kalau `market_positions`/activity diisi cuma lewat insert database manual (tx hash fiktif/acak), modal ini akan gagal fetch — tx hash-nya gak akan pernah ketemu di chain manapun. Supaya ada isinya waktu di-demo di testnet, **baris activity yang di-seed wajib punya transaksi asli yang benar-benar terkirim ke smart contract**, bukan cuma data karangan di database.

Ini berbeda dari prinsip seed di project lain (yang harus DB-only tanpa sentuh onchain) — di sana onchain record mengklaim "AI membuat keputusan nyata", jadi data seed gak boleh ikut commit onchain karena itu klaim palsu. Di Omen, activity feed hanya mencatat "wallet ambil posisi di market" — mengirim transaksi test asli ke kontrak yang sama seperti user beneran pakai itu sah, bukan klaim palsu apa pun.

### Alur Script yang Disarankan (`scripts/seed-testnet-activity.ts`)
1. Siapkan 2-3 wallet test terpisah (BUKAN wallet deployer/admin) yang sudah diisi test-ETH dari faucet, untuk masing-masing chain (Sepolia & Robinhood Chain Testnet) — biar Activity Feed kelihatan ada beberapa "actor" berbeda, bukan 1 wallet yang sama terus.
2. Ambil beberapa market yang sudah ada/di-seed di database (`markets` table, status `OPEN`).
3. Untuk tiap wallet test, panggil fungsi asli di kontrak (`placeBet`/`stakeBelief` — sesuaikan nama fungsi yang benar di `OmenMarket.sol`) dengan jumlah kecil (misal `0.001–0.01 ETH`), gantian sisi AGREE/DISAGREE, ke market-market yang sudah dipilih.
4. Tunggu konfirmasi tx, ambil `txHash` + `blockNumber` + `chainId` yang ASLI dari hasil transaksi tersebut.
5. Insert ke tabel `market_positions`/activity source dengan `txHash` asli itu — supaya nanti modal Bagian A bisa fetch & decode beneran, bukan gagal not-found.
6. Ulangi proses yang sama untuk kedua chain (Sepolia dan Robinhood Chain Testnet) — jangan cuma satu, karena Activity Feed harus bisa demo dari dua-duanya (lihat Definition of Done Bagian A).

### Catatan Keamanan
- Private key wallet seed ini **taruh di env var terpisah** (`SEED_WALLET_PRIVATE_KEY_1`, dst), jangan dicampur sama `ADMIN_WALLET`/`DEPLOYER_KEY` yang dipakai untuk fungsi privileged.
- Script ini idealnya cuma dijalankan manual sekali (atau lewat perintah eksplisit), **bukan bagian dari cron/auto-run production** — karena tujuannya murni ngisi data demo di testnet.
- Jumlah stake per transaksi dibuat kecil, secukupnya buat demo (gak perlu besar), supaya hemat test-ETH dari faucet.

### Definition of Done — Bagian C
- [ ] Ada script `scripts/seed-testnet-activity.ts` yang mengirim transaksi asli (bukan insert DB langsung) ke kontrak market di kedua chain.
- [ ] Setiap baris activity hasil seed punya `txHash` yang valid dan bisa dibuka di block explorer sungguhan.
- [ ] Modal "On-Chain Transaction Receipt" (Bagian A) berhasil menampilkan decoded calldata dari transaksi hasil seed ini tanpa error not-found.
- [ ] Wallet yang dipakai buat seed terpisah dari wallet admin/deployer.
