---
id: TICKET-123
title: Dynamic Gas Estimation and Factory Client Optimization
status: Done
priority: High
labels: [Backend, Web3, SmartContract, BugFix]
---

# Deskripsi
Transaksi pembuatan pasar on-chain melalui `OmenFactory` sebelumnya menggunakan batas gas statis (`gas: 2000000n`). Ketika base fee jaringan Sepolia melonjak naik (~2.38 Gwei), node RPC memvalidasi `cost = gas * gas fee + value` secara pre-flight dan menolak transaksi dengan error `"The total cost of executing this transaction exceeds the balance of the account"` karena nilai kebutuhan gas yang diminta melebihi saldo akun admin. Di samping itu, terdapat bug referensi `gasLimit` di luar blok `try-catch` dan kebutuhan pembulatan bilangan bulat pada parameter target price.

Tiket ini mengimplementasikan estimasi gas dinamis via `publicClient.estimateContractGas(...)` dengan safety buffer 10%, fallback terkalibrasi, scoping variabel yang aman, serta explicit RPC transports untuk Ethereum Sepolia dan Robinhood Chain Testnet.

## Acceptance Criteria (Kriteria Penerimaan)
- [x] Mengganti hardcoded gas limit 2,000,000 dengan estimasi dinamis `publicClient.estimateContractGas` ditambah 10% safety buffer (`(estimated * 110n) / 100n`).
- [x] Menetapkan fallback gas limit aman (1,750,000) jika estimasi RPC mengalami kegagalan.
- [x] Memperbaiki cakupan (*scope*) deklarasi variabel `gasLimit` di `web/lib/market/factory-client.ts` agar tidak menyebabkan compile error `Cannot find name 'gasLimit'`.
- [x] Memastikan parameter target price diubah ke `BigInt(Math.round(num))` untuk mencegah error floating point pada ABI encoder.
- [x] Mengonfigurasi explicit RPC transport menggunakan `process.env.ETHEREUM_SEPOLIA_RPC_URL` dan `process.env.ROBINHOOD_TESTNET_RPC_URL`.
- [x] Seluruh unit test suite lulus (348/348 tests) dan transaksi pembuatan pasar on-chain sukses dieksekusi di testnet.

## Target Lingkup File (Affected Files)
- `omen/web/lib/market/factory-client.ts`
- `omen/web/tests/admin-create-market.test.ts`
- `omen/web/tests/contracts-abi.test.ts`

---

## AI Execution Log dan Output

- **Langkah Teknis Tereksekusi:**
  1. Memperbarui `createOnChainMarket` di `web/lib/market/factory-client.ts` untuk menginisialisasi variabel `gasLimit: bigint = 1750000n` di tingkat fungsi utama sebelum blok simulasi.
  2. Menambahkan pemanggilan `publicClient.estimateContractGas` dengan argumen lengkap `OmenFactory` dan memperhitungkan buffer 10%.
  3. Memperbaiki konversi `targetPrice` numerik menjadi integer bulat sebelum di-*cast* ke `BigInt`.
  4. Mengonfigurasi instance `createPublicClient` dengan explicit HTTP transport url dari environment variables.
  5. Menjalankan pengujian Vitest dan memverifikasi integrasi live on-chain.

- **Ringkasan File Terpengaruh:**
  - `omen/web/lib/market/factory-client.ts`

- **Catatan dan Keputusan Arsitektural:**
  - Estimasi gas dinamis menurunkan kebutuhan *upfront ETH balance* pre-flight check dari ~0.00477 ETH menjadi ~0.0039-0.00408 ETH, memungkinkan akun admin testnet mengeksekusi deployment kontrak pasar tanpa kegagalan saldo.
