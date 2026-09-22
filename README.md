# Dashboard WebGIS Sebaran Genangan Banjir Kota Pontianak

**Penelitian**: Analisis Time-Series NDWI untuk Identifikasi Daerah Rawan Banjir di Kota Pontianak  
**Peneliti**: Gemilang | Universitas Tanjungpura  
**Periode Data**: 2019 - 2024

---

## Cara Membuka Dashboard

1. Buka folder webgis_dashboard/
2. Double-click file **index.html**
3. Pastikan ada koneksi internet (untuk memuat peta dasar Leaflet.js)

## Struktur Folder

`
webgis_dashboard/
|-- index.html              <- Dashboard utama (buka ini!)
|-- data/
|   |-- kerawanan_banjir.geojson   <- Layer kerawanan banjir per kecamatan
|   |-- batas_kecamatan.geojson    <- Batas wilayah kecamatan
|-- assets/                <- Aset tambahan (logo, dll)
`

## Cara Mengganti dengan Data Asli (dari QGIS/GEE)

Anda perlu mengganti file GeoJSON di folder data/ dengan data hasil penelitian asli.

### Langkah Ekspor dari QGIS:
1. Di QGIS, klik kanan layer peta kerawanan banjir Anda
2. Pilih **Export > Save Features As...**
3. Format: **GeoJSON**
4. CRS: **WGS 84 (EPSG:4326)**
5. Simpan sebagai kerawanan_banjir.geojson
6. Simpan sebagai atas_kecamatan.geojson untuk batas kecamatan
7. Ganti file di folder data/

### Format GeoJSON yang Dibutuhkan

**kerawanan_banjir.geojson** - harus memiliki field:
- KECAMATAN - nama kecamatan
- KELAS - "Rawan Tinggi", "Rawan Sedang", atau "Rawan Rendah"
- NDWI_MEAN - nilai NDWI rata-rata
- NDWI_MAX - nilai NDWI maksimum
- LUAS_HA - luas area dalam hektare

**batas_kecamatan.geojson** - harus memiliki field:
- KECAMATAN - nama kecamatan
- LUAS_KM2 - luas dalam km persegi
- PENDUDUK - jumlah penduduk
- NDWI_MEAN - nilai NDWI rata-rata
- KERAWANAN - kelas kerawanan
- LUAS_RAWAN_HA - luas rawan dalam hektare
- PCT_RAWAN - persentase rawan
- KETERANGAN - keterangan detail

## Fitur Dashboard

- Peta interaktif dengan layer kerawanan banjir (Rawan Tinggi/Sedang/Rendah)
- Toggle basemap: OpenStreetMap, Satelit, Topografi, Dark Mode
- Filter kerawanan per kelas
- Kontrol transparansi layer
- Panel statistik per kecamatan
- Grafik Time-Series NDWI 2019-2024 interaktif
- Info detail kecamatan saat diklik di peta
- Koordinat real-time di bawah peta

---
*Dashboard ini dibuat sebagai luaran akhir penelitian skripsi menggunakan Leaflet.js dan Chart.js*
