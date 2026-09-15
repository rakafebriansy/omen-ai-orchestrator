---
id: TICKET-17
title: Pembuatan Komponen Tombol Klaim Payout
status: Todo
priority: High
labels: [Frontend, UI]
---

# Deskripsi
Membangun komponen tombol penarikan hadiah kemenangan `ClaimPayoutButton` di `omen/web/components/ClaimPayoutButton.tsx` dengan indikator saldo reward yang siap dicairkan.

## Spesifikasi Desain dan Teknis (UI / Technical Specification)
### Spesifikasi Antarmuka Komponen (`ClaimPayoutButton.tsx`)
1. **State Siap Klaim (Claimable):**
   - Tombol aktif `bg-yes-green text-white hover:bg-emerald-600 px-4 py-2 rounded-lg font-bold text-xs font-mono shadow-xs transition-all flex items-center gap-1.5`.
   - Teks: "Claim 0.42 ETH".
2. **State Memproses (Claiming):**
   - Tombol disabled dengan spinner loading berputar dan teks "Claiming...".
3. **State Sudah Diklaim (Claimed):**
   - Badge pasif `bg-bg-subtle text-text-muted border border-border-subtle px-3 py-1.5 rounded-lg text-xs font-medium` berlabel "Claimed".

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Tombol aktif khusus untuk posisi taruhan menang yang belum ditarik.
- [ ] Menampilkan estimasi jumlah dana ETH yang akan diklaim.
- [ ] Unit test komponen ClaimPayoutButton lulus pengujian Vitest.

## Target Lingkup File (Affected Files)
- `omen/web/components/ClaimPayoutButton.tsx`
- `omen/web/tests/claim-button.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
