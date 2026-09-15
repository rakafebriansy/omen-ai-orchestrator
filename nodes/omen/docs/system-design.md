# System Design — Omen

Dokumen ini mendefinisikan arsitektur sistem, skema basis data Supabase, spesifikasi antarmuka smart contract `PredictionMarket.sol`, alur integrasi API Next.js, dan protokol pengujian untuk node **Omen**.

---

## 1. Ikhtisar Arsitektur (*Architecture Overview*)

Omen mengadopsi arsitektur *Hybrid Web3*:
* **Lapisan Finansial (On-Chain):** Seluruh taruhan dan payout dikelola langsung oleh smart contract Solidity yang di-deploy di testnet EVM (Arbitrum Sepolia / Robinhood Chain).
* **Lapisan Operasional & Gamifikasi (Off-Chain):** Metadata pasar, tugas harian (*quests*), *daily streak*, dan akumulasi poin dikelola oleh Next.js Serverless Route Handlers dan disimpan di **Supabase PostgreSQL**.

```
+-------------------------------------------------------------------------------+
|                                 Client Browser                                |
|  - Next.js 14+ / 16+ React 19 UI (Tailwind OpenZeppelin Institutional Theme)  |
|  - Phantom Wallet (EVM Mode) via wagmi & viem                                 |
+-----------------------+-------------------------------+-----------------------+
                        | (HTTPS REST / RPC)            | (Web3 Tx via JSON-RPC)
                        v                               v
+-----------------------------------------------+ +-----------------------------+
|        Next.js Route Handlers (Vercel)        | |    PredictionMarket.sol     |
|  - /api/wallet/connect (Upsert User)          | |    (Arbitrum Sepolia)       |
|  - /api/checkin (Daily streak counter)        | |  - createMarket()           |
|  - /api/quests & /api/quests/:id/complete     | |  - placeBet{value}()        |
|  - /api/leaderboard/points                    | |  - resolveMarket()          |
|  - /api/markets (GET list, POST create/resolve| |  - claim()                  |
|  - /api/bets/index (Index on-chain bet event) | |  - refund()                 |
+-----------------------+-----------------------+ +-----------------------------+
                        |
                        | (Supabase JS Client)
                        v
+-----------------------------------------------+
|               Supabase Database               |
|   (PostgreSQL: users, quests, points, bets)   |
+-----------------------------------------------+
```

---

## 2. Diagram Arsitektur Teknis (PlantUML)

Seluruh rancangan arsitektur dimodelkan secara visual menggunakan PlantUML:

1. **Entity Relationship Diagram (ERD):** [erd.puml](./diagrams/erd.puml)
2. **Flowchart Pipeline Taruhan & Poin:** [flowchart.puml](./diagrams/flowchart.puml)
3. **State Machine Siklus Hidup Pasar:** [state-diagram.puml](./diagrams/state-diagram.puml)
4. **Sequence Diagram Alur Taruhan & Klaim:** [sequence-diagram.puml](./diagrams/sequence-diagram.puml)

---

## 3. Desain Basis Data Supabase (*Database Schema*)

### 3.1 Skema Tabel Inti
* `users`: Menyimpan profil wallet, akumulasi `total_points`, timestamp `last_checkin_at`, dan `streak_count`.
* `quests`: Direktori misi/tugas (`title`, `description`, `points_reward`, `is_active`).
* `points_events`: Log audit setiap transaksi masuknya poin (`wallet_address`, `quest_id`, `source`, `points`, `created_at`).
* `markets`: Cache metadata pasar prediksi (`contract_market_id`, `title`, `description`, `deadline`, `status`, `total_pool_yes`, `total_pool_no`, `resolution_source`).
* `bets`: Catatan taruhan pengguna (`market_id`, `wallet_address`, `side`, `amount`, `claimed`, `tx_hash`).

### 3.2 Standar Penyimpanan Datetime
Sesuai panduan `global-guidelines/database.md`:
* Semua kolom waktu (`created_at`, `deadline`, `last_checkin_at`) **WAJIB** menggunakan tipe data `TIMESTAMPTZ` dalam zona waktu UTC.

---

## 4. Spesifikasi Smart Contract (`PredictionMarket.sol`)

Smart contract dikembangkan di `omen/contracts/` menggunakan Solidity `^0.8.20` dengan standar OpenZeppelin `Ownable` dan `ReentrancyGuard`.

### 4.1 State Variables & Structs
```solidity
enum MarketStatus { Active, ResolvedYes, ResolvedNo, Cancelled }

struct Market {
    uint256 id;
    string title;
    uint256 deadline;
    uint256 totalYesPool;
    uint256 totalNoPool;
    MarketStatus status;
    bool exists;
}

struct UserBet {
    uint256 yesAmount;
    uint256 noAmount;
    bool claimed;
}
```

### 4.2 Fungsi Utama
1. `createMarket(string calldata title, uint256 deadline) external onlyOwner returns (uint256)`: Mendaftarkan pasar baru.
2. `placeBet(uint256 marketId, bool side) external payable nonReentrant`: Memasang taruhan dalam Native ETH.
3. `resolveMarket(uint256 marketId, bool result) external onlyOwner nonReentrant`: Mengunci pemenang (Yes/No).
4. `claim(uint256 marketId) external nonReentrant`: Menghitung dan mentransfer payout proporsional kepada pemenang.
5. `cancelMarket(uint256 marketId) external onlyOwner`: Membatalkan pasar dan membuka hak refund.

---

## 5. Arsitektur API Endpoint (*API Routing Architecture*)

| Endpoint | Metode | Akses | Deskripsi |
|---|---|---|---|
| `/api/wallet/connect` | POST | Public | Upsert record user berdasarkan koneksi wallet |
| `/api/checkin` | POST | Authenticated | Klaim poin daily check-in & pembaruan streak |
| `/api/quests` | GET | Authenticated | Mengambil daftar misi aktif beserta status penyelesaian |
| `/api/quests/[id]/complete` | POST | Authenticated | Memvalidasi dan menandai misi selesai |
| `/api/leaderboard/points` | GET | Public | Mengambil ranking global wallet berdasarkan poin |
| `/api/markets` | GET | Public | Mengambil daftar pasar prediksi aktif & riwayat |
| `/api/markets` | POST | Admin Only | Mendaftarkan metadata pasar baru pasca pembuatan on-chain |
| `/api/markets/[id]/resolve` | POST | Admin Only | Memperbarui status pasar pasca resolusi on-chain |
| `/api/bets` | GET | Authenticated | Mengambil riwayat taruhan milik pengguna |
| `/api/bets/index` | POST | Public / Web3 Hook | Merekam event taruhan baru dan memberikan poin partisipasi |

---

## 6. Prosedur Uji Coba & Deployment Testnet (*Testnet-First Policy*)

1. **Unit Testing Hardhat:** Seluruh test suite di `omen/contracts/test/` **WAJIB** mencapai 100% kelulusan (menguji skenario: normal bet, odds distribution, edge cases pool nol di salah satu sisi, unauthorized resolution, reentrancy prevention).
2. **Deploy Testnet:** Deploy ke **Arbitrum Sepolia** menggunakan script `scripts/deploy.ts`. Simpan address kontrak dan ABI ke `omen/web/lib/contracts.ts`.
3. **Frontend Integration:** Uji coba end-to-end (Connect Phantom -> Bet -> Resolve -> Claim) di browser sebelum persiapan mainnet.
