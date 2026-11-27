{
  "name": "kko-bapenda-bondowoso",
  "version": "1.0.0",
  "description": "Aplikasi Mobile Kartu Kendali Omset (KKO) - BAPENDA Kabupaten Bondowoso",
  "scripts": {
    "build:web": "mkdir -p www && cp kko-bapenda-bondowoso.html www/index.html",
    "android:init": "npm run build:web && npx cap add android",
    "android:sync": "npm run build:web && npx cap sync android"
  },
  "dependencies": {
    "@capacitor/android": "^6.1.2",
    "@capacitor/camera": "^6.0.2",
    "@capacitor/core": "^6.1.2",
    "@capacitor/filesystem": "^6.0.1",
    "@capacitor/geolocation": "^6.0.1"
  },
  "devDependencies": {
    "@capacitor/cli": "^6.1.2"
  }
}