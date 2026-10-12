# IoT Flood Monitor

Frontend mengikuti **Frontend Web Development Standard Stack PT. LSKK v1.0**.

## Stack (Mandatory Rules)
| Kebutuhan | Library |
|---|---|
| Bahasa | TypeScript |
| Library | React JS (Functional Components) |
| Bundler | Vite |
| CSS | Tailwind CSS |
| UI Components | Ant Design |
| Table | React Data Grid (MUI X) |
| Data Fetching | Axios |
| Data Query | TanStack Query |
| Global State | Context + Zustand |
| Router | React Router DOM (`createHashRouter`) |
| Formatter / Linter | Prettier / ESLint bawaan Vite |
| Form / Schema | React Hook Form + Zod |

Prinsip: Mobile First (responsive), wajib pakai type/interface/enum, minimalkan `any`.

## Struktur
```
src/
  api/        axios instance & pemanggilan API
  components/ komponen UI (StatusCard di-memoize)
  context/    React Context (ThemeContext)
  hooks/      custom hooks (TanStack Query)
  pages/      halaman (lazy loaded di router)
  router/     createHashRouter + lazy loading
  schemas/    skema Zod
  stores/     Zustand store
  types/      interface & enum (IResponseEntity<T>, ImetaPagination)
```

## Menjalankan
```bash
npm install
cp .env.example .env   # VITE_USE_MOCK=true -> pakai data contoh, login menerima kredensial apa saja
npm run dev
```

## Peta, cuaca, dan jam (data nyata)
- **Peta:** Leaflet + react-leaflet. Tile OpenStreetMap (Peta) dan Esri World Imagery (Satelit); posisi sensor memakai koordinat `lat`/`lng` asli dari API.
- **Garis sungai / batas kecamatan:** diambil dari OpenStreetMap via Overpass API (hanya saat layer dinyalakan, hasil di-cache 24 jam).
- **Radar hujan:** RainViewer (frame terbaru, di-refresh tiap 5 menit).
- **Cuaca:** Open-Meteo (tanpa API key) berdasarkan lokasi: posisi pengguna (tombol "Lokasi saya") > sensor yang dipilih > pusat Kota Semarang. Nama tempat dari Nominatim (reverse geocoding).
- **Jam:** real-time, diperbarui tiap detik mengikuti zona waktu perangkat.
- Semua layanan di atas dipanggil langsung dari browser sehingga butuh koneksi internet.
