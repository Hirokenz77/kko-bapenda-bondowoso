# Panduan Kompilasi Otomatis APK Android — KKO BAPENDA Bondowoso

Seluruh file proyek sudah disiapkan agar dapat dikompilasi menjadi berkas **`.apk` Android murni** secara gratis tanpa perlu menginstal Android Studio di komputer Anda.

## Struktur Folder Repositori
Simpan file-file berikut dalam satu folder/repositori GitHub:
```text
kko-bapenda-bondowoso/
├── kko-bapenda-bondowoso.html   (File utama aplikasi KKO)
├── package.json                 (Dependensi Capacitor, Kamera, GPS, Filesystem)
├── capacitor.config.json        (Identitas aplikasi: go.id.bondowosokab.bapenda.kko)
└── .github/
    └── workflows/
        └── build-apk.yml        (Skrip otomatis pembuat file .apk)
```

## Langkah Mendapatkan File `.apk` (5 Menit)
1. Buat repositori baru di **GitHub** (bisa *Private* maupun *Public*).
2. Unggah keempat file di atas sesuai struktur folder tersebut.
3. Buka tab **Actions** di repositori GitHub Anda, lalu pilih alur kerja **"Build APK Android KKO BAPENDA Bondowoso"** (otomatis berjalan saat file diunggah).
4. Setelah proses selesai (sekitar 2–3 menit, ditandai centang hijau ✓), gulir ke bagian bawah halaman workflow pada bagian **Artifacts** dan klik **`KKO-Bapenda-Bondowoso-APK`**.
5. Ekstrak file ZIP tersebut, dan Anda akan mendapatkan **`KKO-Bapenda-Bondowoso.apk`** yang siap dibagikan ke seluruh HP Android petugas lapangan BAPENDA Bondowoso.

## Fitur yang Sudah Ditanamkan di Dalam APK
* **100% Aset Lokal Offline:** Skrip CSS dibundel secara otomatis ke dalam folder `www/` saat proses build sehingga tampilan tetap rapi meskipun HP petugas berada di area blank-spot sinyal (seperti kawasan Kawah Ijen, Botolinggo, atau Sumberwringin).
* **Izin Native GPS & Kamera:** `AndroidManifest.xml` otomatis disuntikkan izin `ACCESS_FINE_LOCATION` dan `CAMERA` untuk geotagging koordinat dan watermark foto lapangan.