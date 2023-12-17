---
title: Berkenalan Dengan Progressive Web App
date: 2017-10-19 07:24:00 +0000
categories:
- programming
tags:
- Progressive Web App
- Google
excerpt: Pada bulan lalu Google mengadakan Roadshow PWA dimana yang diselenggarakan
  cuman ada di Jakarta dan Yogyakarta, speakersnya di import langsung oleh Google.
  PWA atau Progressive Web Apps adalah aplikasi web yang menggunakan teknologi terkini
  yang seakan-akan seperti aplikasi Native App (Android/iOS)
image: "/uploads/progressive-web-apps.png"

---
Pada bulan lalu Google mengadakan Roadshow PWA dimana yang diselenggarakan cuman ada di Jakarta dan Yogyakarta, speakersnya di import langsung oleh Google. PWA atau Progressive Web Apps adalah aplikasi web yang menggunakan teknologi terkini yang seakan-akan seperti aplikasi Native App (Android/iOS).

Native Apps dapat **berjalan secara offline, mengirim Push Notifications, load** dengan cepat, dan **dapat dibuka melalui Home screen**. Teknologi PWA menggunakan **SPA** (Single Page Application) seperti VueJS, AngularJS, Polymer, Preact, React atau lainnya. 

## Apa itu SPA
Single page application (SPA) adalah istilah untuk aplikasi berbasis web, yang menggunakan satu halaman web saja sebagai tampilan dari aplikasinya. Semua aksi klik atau pun penyajian data tidak akan membuat halaman secara utuh dimuat ulang (reload), tetapi hanya beberapa saja yang diupdate dari server atau dari hasil proses aplikasi di sisi klien. Akibat dari penggunaan teknologi ini menjadikan web yang dibuat menjadi lebih ringan dan lebih cepat ketika digunakan.

![Image](https://developers.kudo.co.id/wp-content/uploads/2016/11/Single-Page-Application.png)

Teknologi SPA ini menggunakan javascript sebagai alat utamanya dan HTML5 & CSS3 sebagai pendukungnya. HTML5 & CSS3 digunakan untuk membentuk layout dan mempercantik halamannya. Javascript untuk perubahan halaman serta alat komunikasi dengan server. Adapun teknik yang digunakan dari javascript itu ada yang menggunakan AJAX, beberapa aplikasi modern yang memerlukan komunikasi data realtime seperti aplikasi chat, WebSocket digunakan sebagai protokol yang lebih cepat dan ringan. Ada juga yang menggunakan framework yang sudah ada seperti angularjs atau knockoutjs atau menggunakan view library serperti ReactJs.

## Kembali lagi
Menurut data dari Google, 53% orang akan meninggalkan halaman jika memakan waktu lebih dari 3 detik untuk memuat halaman.

![Image](https://cdn-images-1.medium.com/max/800/1*pYOjmBQun9HhaiXne79Y6w.png)

Disinilah Service Worker memberi jawaban untuk masalah ini, kita akan menyimpan shell (Kerangka Halaman) dan Assets (CSS & JS) di Cache Storage yang nantinya akan ditampilkan kepada user. Jadi user tidak perlu mendownload ulang terus-menerus setiap reload halaman, dan bahkan bisa ditampilkan ketika user sedang offline.

![Image](https://cdn-images-1.medium.com/max/800/1*3JVbZ8I5Ch2DvGOysu2-Mg.jpeg)

Karena disimpan di dalam Cache Storage jadi user hanya perlu mendownload halaman kita sekali saja dan setelah itu user tidak perlu lagi untuk mendownload shell dan assets kita setiap user membuka halaman web. 

## Cara Kerja Service Worker

![Image](https://cdn-images-1.medium.com/max/800/1*3JVbZ8I5Ch2DvGOysu2-Mg.jpeg)

Penjelasan Cara Kerja Service Worker:

1. Kita asumsikan bawa user belum pernah mengunjungi web kita. Ketika user melakukan request dan melewati SW(Service Worker), SW akan mengecek terlebih dahulu, apakah file sudah tersedia di dalam Cache Storage? Karena ini pertama kalinya user mengunjungi halaman kita, maka SW akan mengarahkan request ke web server dan SW juga akan menyimpan file yang sudah di download ke dalam Cache Storage.

2. Kini shell & assets sudah tersimpan dalam Cache Storage, untuk request selanjutnya sama seperti diatas, request akan melewati SW, dan SW akan mengecek terlebih dahulu di Cache Storage. Karena assets dan shell sudah tersedia di Cache Storage, maka SW akan otomatis mengirimkan file dari Cache Storage untuk ditampilkan ke user.

![Image](https://cdn-images-1.medium.com/max/800/1*0DbLk6XBVLI7tVct_OUboQ.png)

Jadi SW bertugas sebagai proxy (sebagai perantara browser dan jaringan internet). Karena kemampan kontrol terhadap request dan response yang seperti ini, maka syarat untuk dapat menggunakan Service Worker adalah aplikasi web harus menggunakan https agar lebih aman.

**Refrensi:**

* [https://medium.com/wwwid/pengenalan-progressive-web-app-pwa-bagian-1-cac0fadbe5f4](https://medium.com/wwwid/pengenalan-progressive-web-app-pwa-bagian-1-cac0fadbe5f4)
* [https://medium.com/hammercode/berkenalan-dengan-service-worker-578a45951df7](https://medium.com/hammercode/berkenalan-dengan-service-worker-578a45951df7)
* [https://medium.com/@eezhal92/tutorial-defer-operasi-ketika-koneksi-internet-tidak-stabil-dengan-background-sync-d5e4624f30af](https://medium.com/@eezhal92/tutorial-defer-operasi-ketika-koneksi-internet-tidak-stabil-dengan-background-sync-d5e4624f30af)