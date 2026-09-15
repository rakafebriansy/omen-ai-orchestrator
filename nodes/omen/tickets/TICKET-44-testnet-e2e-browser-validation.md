---
id: TICKET-44
title: Validasi Siklus Hidup Penuh End-to-End di Browser
status: Todo
priority: High
labels: [QA, E2E, Web3]
---

# Deskripsi
Menjalankan uji coba validasi siklus hidup penuh (End-to-End) aplikasi Omen pada lingkungan browser testnet Arbitrum Sepolia.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Skenario Alur E2E
1. **Koneksi dan Onboarding:** Connect Phantom Wallet -> Auto-register user -> Selesaikan Daily Check-in -> Selesaikan 1 misi quest -> Verifikasi poin bertambah.
2. **Pembuatan Pasar:** Admin login -> Buat pasar prediksi baru on-chain -> Verifikasi pasar muncul di katalog.
3. **Pemasangan Taruhan:** Bettor 1 pasang Yes (0.05 ETH) -> Bettor 2 pasang No (0.05 ETH) -> Verifikasi pool ratio bar 50/50 dan bonus poin partisipasi.
4. **Resolusi dan Klaim:** Deadline terlewati -> Admin resolve YES -> Bettor 1 klik Claim Payout -> Verifikasi dana 0.10 ETH masuk ke dompet Bettor 1.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Seluruh skenario siklus penuh berhasil dieksekusi tanpa kendala dana macet.
- [ ] Poin gamifikasi dan peringkat leaderboard terbarui secara akurat.
- [ ] Dokumentasi laporan pengujian E2E tercatat lengkap.

## Target Lingkup File (Affected Files)
- `omen/web/tests/e2e/workflow.test.ts`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
