---
id: TICKET-56
title: Integrasi Real Wagmi Web3 Wallet Connection (Phantom/MetaMask) & Network Switcher
status: Todo
priority: High
labels: [Frontend, Web3, Wallet, Wagmi, LiveOnChain]
---

# Deskripsi
Setelah deployment smart contract ke Arbitrum Sepolia selesai pada TICKET-55, tiket ini bertugas mengaktifkan mode wallet nyata via Wagmi connector (Phantom EVM & Injected Provider), dialog perpindahan chain (Arbitrum Sepolia Chain ID 421614), dan sinkronisasi saldo live ETH pengguna.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Menghubungkan Wagmi hooks `useAccount`, `useConnect`, `useDisconnect`, `useBalance` ke `ConnectWalletButton.tsx`.
- [ ] Dialog `NetworkSwitcherModal.tsx` memicu `useSwitchChain` ke Arbitrum Sepolia jika dompet terhubung ke chain lain.
- [ ] Sinkronisasi otomatis alamat wallet aktif ke Supabase via `POST /api/wallet/connect`.

## Target Lingkup File (Affected Files)
- `omen/web/components/ConnectWalletButton.tsx`
- `omen/web/components/NetworkSwitcherModal.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. Draf tiket live wallet connection dibuat.
- **Ringkasan File Terpengaruh:**
  - `omen/web/components/ConnectWalletButton.tsx`
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
  - Aktif saat `NEXT_PUBLIC_USE_MOCK_CONTRACT="false"`.
