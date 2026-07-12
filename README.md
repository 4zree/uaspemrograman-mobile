# KampusMarket 🎓🛍️

MVP aplikasi marketplace jual-beli barang bekas mahasiswa, dibuat untuk memenuhi
Ujian Akhir Semester (UAS) Praktikum Pemrograman Mobile — React Native & Expo,
Program Studi Teknik Informatika, Universitas Islam Riau.

Data produk & simulasi login memakai API publik **[DummyJSON](https://dummyjson.com)**
— tidak ada backend sendiri, sesuai ketentuan soal.

## ✅ Checklist Ketentuan Wajib

| Aspek | Implementasi |
|---|---|
| **Layout (Flexbox)** | 3 halaman utama: `LoginScreen`, `HomeScreen` (Katalog), `ProductDetailScreen`. Semua layout memakai Flexbox & `SafeAreaView` sehingga otomatis menyesuaikan ukuran layar HP. |
| **Komponen** | 5 komponen reusable di `src/components`: `AppButton`, `InputField`, `ProductCard`, `CategoryChip`, `StatusView`. |
| **Lists** | `FlatList` 2 kolom di `HomeScreen` dan `FlatList` di `CartScreen`, dengan `initialNumToRender`, `windowSize`, `removeClippedSubviews` supaya tetap ringan. |
| **State & Hooks** | Pencarian (`useState` + debounce 300ms) dan filter kategori di `HomeScreen`, sehingga daftar produk otomatis berubah tanpa membuat aplikasi lag. |
| **Form** | `LoginScreen` & `RegisterScreen` dengan validasi nama, format email (regex), panjang password minimal 6 karakter, dan konfirmasi password — lihat `src/utils/validators.js`. |
| **Navigasi** | Bottom tab navigation (Home, Wishlist, Profil) via `MainTabs`. Home → Detail Produk via stack (`HomeStack`). Wajib login dulu — diatur otomatis oleh `RootNavigator` berdasarkan status `AuthContext`. |
| **API** | Semua request di `src/api/dummyjson.js`. Status *loading / success / error* ditampilkan jelas lewat komponen `StatusView`, lengkap dengan tombol "Coba Lagi" agar aplikasi tidak crash saat gagal fetch. |

## 📁 Struktur Folder

```
KampusMarket/
├── App.js
├── app.json
├── package.json
├── assets/                  # icon & splash
└── src/
    ├── api/dummyjson.js     # semua request ke DummyJSON
    ├── components/          # komponen reusable
    ├── context/             # AuthContext & CartContext (state global)
    ├── navigation/          # RootNavigator, AuthNavigator, MainTabs, HomeStack
    ├── screens/             # Login, Register, Home, ProductDetail, Cart, Profile
    └── utils/validators.js  # validasi form
```

## 🚀 Cara Menjalankan (Expo Go)

Project ini dibuat dengan **Expo SDK 54**, yaitu versi yang saat ini didukung
oleh aplikasi **Expo Go** di Play Store / App Store (per Juli 2026). Catatan:
penomoran "Expo Go versi 5.4" pada aplikasi store sebenarnya mengikuti nomor
SDK (mis. SDK 54), bukan versi 5.4 tersendiri — project ini sudah disesuaikan
supaya kompatibel dengan Expo Go yang terbaru di store.

### 1. Install dependencies
```bash
cd KampusMarket
npm install
```

### 2. (Disarankan) Samakan versi paket dengan SDK yang terpasang
```bash
npx expo install --fix
```
Perintah ini otomatis mencocokkan versi setiap paket (react-navigation,
react-native-screens, dll) dengan versi Expo SDK yang benar-benar terpasang
di komputer kamu — penting karena versi Expo Go di HP kamu bisa saja sedikit
berbeda dari SDK 54 yang dipakai sebagai basis di sini.

### 3. Jalankan project
```bash
npx expo start
```
Lalu scan QR code yang muncul menggunakan aplikasi **Expo Go** di HP kamu
(Android/iOS harus terhubung ke WiFi yang sama dengan komputer).

### 4. Login
Login sekarang memakai **akun demo lokal** (tidak lagi memanggil API asli
DummyJSON, karena server mereka tidak punya akun bernama "budi"). Sudah
terisi otomatis di form Login:
- **Username:** `budi`
- **Password:** `budi123`

Kredensial ini bisa diganti bebas di satu tempat: `src/context/AuthContext.js`
(konstanta `DEMO_USERNAME` & `DEMO_PASSWORD`).

## 🧠 Catatan Teknis

- **Simulasi login**: memakai akun demo lokal (`src/context/AuthContext.js`),
  tidak memanggil API eksternal, supaya kredensial bisa bebas diatur sendiri
  (mis. username "budi").
- **Simulasi daftar akun**: memakai endpoint `POST /users/add`. DummyJSON
  bersifat *mock* sehingga akun baru tidak benar-benar tersimpan permanen di
  server mereka — karena itu setelah daftar, pengguna diarahkan untuk login
  memakai akun uji yang tersedia.
- **Wishlist/Keranjang** disimpan di memori (React Context), sesuai kebutuhan
  MVP take-home ini.
- **Sesi login** disimpan di `AsyncStorage` supaya tidak perlu login ulang
  setiap membuka aplikasi.

## 📦 Pengumpulan Tugas

Jangan lupa lengkapi sebelum submit:
1. Push project ini ke repository GitHub kamu.
2. Rekam video demo aplikasi berjalan (durasi bebas), unggah ke YouTube/Google Drive.
3. Kumpulkan sebelum tenggat: **09 Juli 2026**.
