# Indonesia GeoJSON

Repository ini berisi data geografis Indonesia dalam format GeoJSON yang mencakup batas wilayah administratif tingkat provinsi dan kabupaten/kota.

## 📁 Struktur File

- **`provinsi.geojson`** - Data batas wilayah 38 provinsi di Indonesia
- **`kab_kota.geojson`** - Data batas wilayah 514 kabupaten dan kota di Indonesia

## 📊 Informasi Data

### Metadata
- **Sumber Data**: [Laravel Nusa](https://nusa.creasi.dev) - [GitHub](https://github.com/creasico/laravel-nusa)
- **Referensi**: Kepmendagri No 300.2.2-2138 Tahun 2025
- **Generator**: [Peta Nusa](https://petanusa.web.id) v1.0
- **Tanggal Generate**: 16 Februari 2026
- **Lisensi**: MIT License

### Cakupan Wilayah
Data mencakup seluruh provinsi di Indonesia:
- Aceh, Bali, Banten, Bengkulu
- DI Yogyakarta, DKI Jakarta
- Gorontalo, Jambi
- Jawa Barat, Jawa Tengah, Jawa Timur
- Kalimantan Barat, Kalimantan Selatan, Kalimantan Tengah, Kalimantan Timur, Kalimantan Utara
- Kepulauan Bangka Belitung, Kepulauan Riau
- Lampung
- Maluku, Maluku Utara
- Nusa Tenggara Barat, Nusa Tenggara Timur
- Papua, Papua Barat, Papua Barat Daya, Papua Pegunungan, Papua Selatan, Papua Tengah
- Riau
- Sulawesi Barat, Sulawesi Selatan, Sulawesi Tengah, Sulawesi Tenggara, Sulawesi Utara
- Sumatera Barat, Sumatera Selatan, Sumatera Utara

## 🗺️ Format Data

### Struktur GeoJSON
Setiap file mengikuti standar GeoJSON dengan struktur:

```json
{
  "type": "FeatureCollection",
  "metadata": {
    "generator": { ... },
    "query": { ... },
    "result": { ... },
    "source": { ... },
    "copyright": { ... }
  },
  "features": [...]
}
```

### Properties untuk Kabupaten/Kota
```json
{
  "code": "11.05",
  "name": "Kabupaten Aceh Barat",
  "level": "regency"
}
```

### Properties untuk Provinsi
```json
{
  "code": "11",
  "name": "Aceh",
  "level": "province"
}
```

## 💻 Cara Penggunaan

### JavaScript
```javascript
// Menggunakan fetch API
fetch('kab_kota.geojson')
  .then(response => response.json())
  .then(data => {
    console.log(`Total kabupaten/kota: ${data.features.length}`);
    // Gunakan data untuk visualisasi peta
  });
```

### Python
```python
import json

# Membaca file GeoJSON
with open('kab_kota.geojson', 'r') as f:
    data = json.load(f)

print(f"Total kabupaten/kota: {len(data['features'])}")

# Contoh: Mendapatkan semua kabupaten di Aceh
aceh_regencies = [
    feature for feature in data['features'] 
    if feature['properties']['code'].startswith('11.')
]
```

### Leaflet.js
```javascript
// Menampilkan peta dengan Leaflet
const map = L.map('map').setView([-2.5, 118], 5);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);

fetch('kab_kota.geojson')
  .then(response => response.json())
  .then(data => {
    L.geoJSON(data, {
      style: {
        color: '#3388ff',
        weight: 2,
        fillOpacity: 0.2
      },
      onEachFeature: (feature, layer) => {
        layer.bindPopup(feature.properties.name);
      }
    }).addTo(map);
  });
```

### Mapbox GL JS
```javascript
map.on('load', () => {
  map.addSource('indonesia', {
    type: 'geojson',
    data: 'kab_kota.geojson'
  });

  map.addLayer({
    id: 'indonesia-layer',
    type: 'fill',
    source: 'indonesia',
    paint: {
      'fill-color': '#088',
      'fill-opacity': 0.4
    }
  });
});
```

## 📦 Ukuran File

| File | Ukuran |
|------|--------|
| `kab_kota.geojson` | ~17 MB |
| `provinsi.geojson` | ~12 MB |

## 🔍 Use Cases

- **Visualisasi Peta**: Menampilkan batas wilayah administratif Indonesia
- **Analisis Geografis**: Analisis spasial dan statistik berbasis wilayah
- **Aplikasi Web/Mobile**: Integrasi peta interaktif dalam aplikasi
- **Dashboard**: Visualisasi data berbasis lokasi
- **GIS Analysis**: Analisis sistem informasi geografis

## 🛠️ Tools yang Kompatibel

- [QGIS](https://qgis.org/)
- [Leaflet](https://leafletjs.com/)
- [Mapbox](https://www.mapbox.com/)
- [Google Maps API](https://developers.google.com/maps)
- [D3.js](https://d3js.org/)
- [Turf.js](https://turfjs.org/)
- [GeoPandas](https://geopandas.org/)

## 📄 Lisensi

Data ini dilisensikan di bawah [MIT License](https://github.com/creasico/laravel-nusa/blob/main/LICENSE).

```
© Creasi.co - Laravel Nusa
```

## 🙏 Kredit

Data bersumber dari:
- **Laravel Nusa**: https://nusa.creasi.dev
- **GitHub**: https://github.com/creasico/laravel-nusa
- **Peta Nusa**: https://petanusa.web.id

## 📞 Kontak & Kontribusi

Jika Anda menemukan kesalahan data atau ingin berkontribusi, silakan kunjungi [repository Laravel Nusa](https://github.com/creasico/laravel-nusa).

---

**Catatan**: Data ini diperbarui berdasarkan Kepmendagri No 300.2.2-2138 Tahun 2025. Pastikan untuk selalu menggunakan data terbaru untuk akurasi maksimal.
