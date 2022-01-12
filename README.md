# Tutorial Setup Tailwind 3 di Proyek Svelte

Tutorial ini berisikan cara menginstall dan mengatur konfigurasi Tailwind versi 3 di proyek Svelte. Pastikan sudah terinstall Nodejs di komputer kalian.

## 1. Buat Proyek Svelte
Buatlah proyek baru dengan perintah di bawah.
```sh
npx degit svelte/template nama-proyek
cd nama-proyek
npm install
```

## 2. Instal Tailwind
Install Tailwind dan Concurrently. Concurrently berfungsi untuk menjalankan perintah npm secara bersamaan, dalam hal ini ialah server lokal Svelte dan Tailwind CLI build process.
```sh
npm i -D tailwindcss concurrently
npx tailwind init
```

## 3. Tambahkan Template Path di tailwind.config.js
Buka file tailwind.config.js, tambahkan script berikut.
```javascript
module.exports = {
  content: ["./src/**/*.{html,js,svelte,ts}"]
  theme: {
    extend: {},
  },
  plugins: [],
}
```

## 4. Buat File tailwind.css
Masuk ke folder public, buat file baru bernama tailwind.css. Tambahkan kode berikut di dalamnya.
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 5. Tambahkan Script di package.json
Di dalam package.json, timpakan kode berikut ke dalamnya.
```javascript
// ...
"scripts": {
  "tailwind:watch": "npx tailwindcss -i ./public/tailwind.css -o ./public/global.css --watch",
  "tailwind:build" : "tailwindcss -o ./public/global.css --minify",
  "build": "npm run tailwind:build && rollup -c",
  "dev": "concurrently \"rollup -c -w\" \"npm run tailwind:watch\"",
  "start": "sirv public --no-clear"
},
// ...
```

## 6. Jalankan `npm run dev`
Setup selesai, sekarang jalankan perintah berikut.
```sh
npm run dev
```

## 7. Coba Untuk Menambahkan Tailwind Class
Cobalah untuk mengbah file App.svelte menjadi seperti berikut.
```html
<main>
  <h1 class="text-blue-500 text-center text-5xl mt-32">Hello World</h1>
  <p class="text-gray-800 text-center mt-4">Visit the <a class="text-blue-400 hover:underline" href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>
```