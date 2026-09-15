# Prototypes Directory — Omen

Direktori `prototypes/` berfungsi sebagai ruang uji coba atau kanvas visual mandiri untuk merancang (*design*) komponen antarmuka (UI) sebelum diimplementasikan ke dalam kerangka kerja Next.js / Tailwind produksi.

## Konsep dan Tujuan Utama

Pendekatan esensial dari folder ini adalah **Rapid HTML-based Previewing**. Seluruh rancangan visual baru dapat disketsa menggunakan teknologi web dasar (**HTML/CSS/Canvas**) di dalam folder ini untuk validasi cepat sebelum ditranslasikan ke komponen React/TypeScript.

## Aturan Ketat Pembuatan Komponen (*Single-File Policy*)
1. **Wajib Single-File (Internal CSS & JS):** Setiap rancangan satu buah komponen atau antarmuka **HARUS** disatukan ke dalam satu *file* berformat `.html` saja.
2. **Dilarang Memecah File Eksternal:** Seluruh gaya elemen wajib ditulis menggunakan *Internal CSS* (`<style>`) dan *Internal JS* (`<script>`).
3. **Hanya Kanvas Visual Statis:** Dilarang menyentuh database produksi atau private keys.
