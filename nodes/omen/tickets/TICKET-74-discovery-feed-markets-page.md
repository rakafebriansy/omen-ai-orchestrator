---
id: TICKET-74
title: Pembuatan Halaman Discovery Feed Pasar Keyakinan (/markets) & Tab Filter
status: Todo
priority: High
labels: [Frontend, UI, Page]
---

# Deskripsi
Halaman Discovery Feed (`app/markets/page.tsx`) adalah katalog penjelajahan pasar keyakinan publik.

Fitur utama halaman ini:
1. **Discovery Tabs**: Tab kurasi pasar: `Trending`, `Newest`, `Ending Soon`, `Most Volume`, dan `Confirmed`. (Sesuai brief, tidak ada algoritma For You / Following di V1).
2. **Search Bar**: Pencarian instan berbasis teks pernyataan belief, handle kreator, atau kategori.
3. **Grid Render**: Menampilkan daftar pasar menggunakan kartu `BeliefMarketCard` dengan layout grid responsif.
4. **Data Fetching**: Terhubung langsung ke endpoint `GET /api/markets` dengan query parameter `tab`, `search`, dan `category`.
5. **Loading & Empty State**: Menampilkan skeleton loader saat data dimuat dan ilustrasi empty state informatif jika tidak ada pasar yang sesuai.

> 🎨 **UI Style Preservation Note:**
> Desain tab pills dengan active highlight, search input box dengan ikon pencarian, skeleton loading shimmer, empty state container, dan tata letak grid kartu **WAJIB DIPERTAHANKAN** sesuai standar estetika antarmuka OMEN.

## Acceptance Criteria (Kriteria Penerimaan)
- [ ] Mengimplementasikan halaman `app/markets/page.tsx` dan komponen filter `DiscoveryFilter.tsx`.
- [ ] Menyediakan tab discovery: `Trending`, `Newest`, `Ending Soon`, `Most Volume`, dan `Confirmed`.
- [ ] Mengambil data live dari endpoint `GET /api/markets` dengan penanganan state loading dan error yang mulus.
- [ ] Mendukung input pencarian teks dan filter kategori.
- [ ] Merender kartu `BeliefMarketCard` dalam grid responsif (1 kolom mobile, 2-3 kolom desktop).
- [ ] Mempertahankan style UI, warna, dan tema OpenZeppelin dark mode existing.
- [ ] Menyusun unit test pada `web/tests/markets-page.test.tsx` dan memastikan lulus 100% dengan Zero-Comment Policy.

## Target Lingkup File (Affected Files)
- `omen/web/app/markets/page.tsx`
- `omen/web/components/DiscoveryFilter.tsx`
- `omen/web/tests/markets-page.test.tsx`

---

## AI Execution Log dan Output
*⚠️ Peringatan untuk AI Agent: Bagian ini KHUSUS diisi oleh Anda SAAT dan SETELAH mengeksekusi tiket ini.*

- **Langkah Teknis Tereksekusi:**
  1. ...
- **Ringkasan File Terpengaruh:**
- **Catatan dan Keputusan Arsitektural (Jika Ada):**
