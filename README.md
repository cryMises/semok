# sêmok

Info kondisi UV dan kualitas udara di Semarang, fokus utama area BINUS @Semarang (Semarang Barat). Satu file HTML, jalan langsung di browser, tanpa server dan tanpa API key.

## Fitur

- **Kesimpulan bahaya** — satu kalimat jelas: aman, santai saja, batasi waktu, atau hindari keluar. Diambil dari kombinasi UV dan AQI, mana yang lebih parah yang menentukan. Ada chip yang menyebut mana yang jadi pemicu.
- **Dua gauge** — Indeks UV dan US AQI lengkap dengan levelnya, plus catatan jam paling ekstrem hari itu.
- **Ringkasan kondisi** — suhu, suhu terasa, kelembapan, cuaca, matahari terbit/terbenam, UV maksimum, AQI maksimum, dan peluang hujan.
- **Peta interaktif** — 6 titik di Semarang (BINUS jadi titik utama, plus Sam Poo Kong, Lawang Sewu, Simpang Lima, Kota Lama, Marina Beach). Tiap titik berwarna sesuai tingkat bahaya, tap untuk lihat angka UV dan AQI di sana. Ada juga daftar titik yang bisa diklik.
- **Cek lokasi saya** — pakai GPS perangkat untuk melihat perkiraan UV dan AQI di tempat Anda sekarang, plus penanda khusus di peta.
- **Grafik 24 jam** — tren UV dan AQI hari ini dengan dua sumbu. Garis penuh untuk data yang sudah terjadi, garis putus-putus untuk perkiraan sisa hari. Tanda matahari terbit/terbenam, penanda "sekarang", dan tooltip kalau ditunjuk.
- **Jam-jam berikutnya** — 12 jam ke depan lengkap dengan UV, AQI, dan peluang hujan.
- **Waktu terbaik keluar** — jendela hingga 2 jam paling nyaman dalam 24 jam ke depan, dipilih otomatis dari data per jam.
- **Rincian polutan** — PM2.5, PM10, ozon, NO₂, SO₂, CO dalam µg/m³, dibandingkan dengan pedoman WHO: ozon rerata 8 jam, polutan lain rerata 24 jam.
- **Saran praktis** — berbeda-beda tergantung apakah UV atau kualitas udara yang jadi masalah.
- **Mode gelap** — mengikuti sistem, bisa diganti manual dan diingat.
- **Update otomatis** tiap 10 menit, lengkap dengan hitung mundur ke update berikutnya.
- **Cadangan data** — kalau API gagal, data terakhir yang berhasil disimpan masih ditampilkan (dengan penanda bahwa datanya sudah lama).

## Sumber data

[Open-Meteo](https://open-meteo.com) — gratis, tanpa API key, tanpa batas request untuk pemakaian wajar.

- `air-quality-api.open-meteo.com` untuk AQI dan polutan
- `api.open-meteo.com/v1/forecast` untuk indeks UV, cuaca, dan matahari terbit/terbenam

Titik utama (BINUS) juga ambil data per jam (`hourly=uv_index`, `hourly=us_aqi`, `hourly=precipitation_probability`) untuk grafik, strip jam-jam berikutnya, dan pencarian waktu terbaik. Lima titik lainnya cuma ambil data saat ini, supaya jumlah request tetap ringan.

## Cara pakai

Buka `index.html` di browser mana saja. Tidak perlu instalasi atau build step.

Untuk hosting, upload filenya ke static hosting apa saja (Netlify, Vercel, GitHub Pages, dan lain-lain).

## Struktur teknis

Satu file `index.html`, semua CSS dan JavaScript inline. Library eksternal:

- [Leaflet 1.9.4](https://leafletjs.com) via unpkg, untuk peta
- [OpenStreetMap](https://www.openstreetmap.org) untuk tile peta
- Google Fonts: Fraunces (judul) dan Inter (teks biasa)

Grafik tren dibuat manual pakai SVG, tanpa library chart.

Motif batik (kawung, zigzag, ceplok) digambar sebagai SVG di dalam `data:` URI dan dipakai lewat `mask-image`, jadi warnanya bisa mengikuti tema terang/gelap tanpa file gambar terpisah.

## Titik koordinat

| Lokasi | Lat | Lon | Keterangan |
|---|---|---|---|
| BINUS @Semarang | -6.9804 | 110.3831 | Titik utama, Tawangsari, Semarang Barat |
| Sam Poo Kong | -6.9963 | 110.3980 | Klenteng, dekat Semarang Barat |
| Lawang Sewu | -6.9839 | 110.4106 | Bangunan bersejarah, pusat kota |
| Simpang Lima | -6.9898 | 110.4229 | Alun-alun pusat kota |
| Kota Lama (Blenduk) | -6.9681 | 110.4275 | Kawasan Kota Lama |
| Marina Beach | -6.9420 | 110.3980 | Pantai utara Semarang |

Koordinat BINUS diambil dari alamat POJ Avenue Kav. 3, Kel. Tawangsari, Kec. Semarang Barat karena tidak ada titik resmi untuk gedungnya.

## Catatan akurasi

- Indeks UV dihitung dari posisi matahari, jadi cukup akurat untuk lokasi manapun.
- Data kualitas udara berbasis model satelit, bukan sensor fisik persis di titik tersebut. Anggap sebagai estimasi wilayah, bukan angka presisi per meter.
- Karena modelnya berbasis grid, beberapa titik yang berdekatan sering menunjukkan angka yang sama.

## Rencana pengembangan

- Riwayat 7 hari terakhir
- Perbandingan antar titik (ranking UV/AQI)
- Bisa diinstall sebagai app (PWA)

## Lisensi data

Data cuaca dan kualitas udara dari Open-Meteo, gratis untuk pemakaian non-komersial. Tile peta dari OpenStreetMap, © kontributor OpenStreetMap.
