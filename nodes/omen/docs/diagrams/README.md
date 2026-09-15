# Arsitektur & Diagram Teknis — Node Omen

Direktori ini memuat seluruh spesifikasi diagram arsitektur PlantUML untuk node `omen`:

1. **[erd.puml](./erd.puml):** Entity Relationship Diagram 5 tabel utama basis data Supabase (`users`, `quests`, `points_events`, `markets`, `bets`).
2. **[flowchart.puml](./flowchart.puml):** Pipeline alur taruhan on-chain, resolusi admin, klaim payout, dan alokasi reward poin.
3. **[state-diagram.puml](./state-diagram.puml):** State machine siklus hidup pasar prediksi (`Created` -> `Active` -> `Locked` -> `Resolved` -> `Claimed`).
4. **[sequence-diagram.puml](./sequence-diagram.puml):** Diagram sekuensial interaksi Pengguna, Frontend Next.js, Smart Contract `PredictionMarket.sol`, dan Backend Supabase.
