name: Build APK Android KKO BAPENDA Bondowoso

on:
  push:
    branches: [ main, master ]
  workflow_dispatch:

jobs:
  build-android-apk:
    runs-on: ubuntu-latest

    steps:
      - name: 1. Checkout Kode Proyek
        uses: actions/checkout@v4

      - name: 2. Siapkan Node.js 20
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: 3. Siapkan Java JDK 17 & Android SDK
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: 4. Install Dependensi Capacitor & Siapkan Folder Web Lokal
        run: |
          npm install
          mkdir -p www
          cp kko-bapenda-bondowoso.html www/index.html
          # Unduh Tailwind CSS lokal agar 100% jalan tanpa internet di dalam APK
          curl -sL https://cdn.tailwindcss.com -o www/tailwind.js
          sed -i 's|https://cdn.tailwindcss.com|tailwind.js|g' www/index.html

      - name: 5. Generate Proyek Native Android & Konfigurasi Izin GPS + Kamera
        run: |
          npx cap add android
          npx cap sync android
          MANIFEST="android/app/src/main/AndroidManifest.xml"
          sed -i '/<application/i \
          <uses-permission android:name="android.permission.INTERNET" />\
          <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />\
          <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />\
          <uses-feature android:name="android.hardware.location.gps" android:required="false" />\
          <uses-permission android:name="android.permission.CAMERA" />\
          <uses-feature android:name="android.hardware.camera" android:required="false" />\
          <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />\
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" android:maxSdkVersion="32" />' "$MANIFEST"

      - name: 6. Build APK Android (Debug / Siap Install)
        run: |
          cd android
          chmod +x gradlew
          ./gradlew assembleDebug
          cp app/build/outputs/apk/debug/app-debug.apk ../KKO-Bapenda-Bondowoso.apk

      - name: 7. Unggah File APK Hasil Build
        uses: actions/upload-artifact@v4
        with:
          name: KKO-Bapenda-Bondowoso-APK
          path: KKO-Bapenda-Bondowoso.apk
          retention-days: 90