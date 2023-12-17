---
title: Persiapan Membuat Aplikasi Android Dengan React Native
date: 2017-10-09 11:12:00 +0000
categories:
- programming
tags:
- React Native
- Android
- Android Studio
- Google
layout: single
excerpt: React Native merupakan framework yang dibuat oleh facebook yang membuat kita
  dapat membuat mobile application (iOS dan Android) menggunakan JavaScript. Saat
  ini, React Native merupakan framework yang sangat populer untuk membuat mobile application.
image: assets/images/posts/reactnative.jpg

---
## Getting Started with React Native on Windows
(Artikel ini ditujukan baru yang ingin memulai membuat aplikasi android dengan react native)

**Android Development Environment**

Tools yang diperlukan untuk membuat dan menjalankan Android dengan React Native kita perlu install tools berikut:

* **Install NodeJS**

    Untuk install node di windows, bisa ikuti link berikut ini : [http://blog.teamtreehouse.com/install-node-js-npm-windows](http://blog.teamtreehouse.com/install-node-js-npm-windows)

* **Install JDK (Java Development Kit)**
[Download JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

* **Install Android Studio**
[Download Android Studio](https://developer.android.com/studio/index.html?hl=id)

* **Download Android SDK yang diperlukan**
    1. Android 6.0 (Marshmallow) SDK (platform 23)
    2. Android SDK build tools 23.0.1, 23.0.2, 23.0.3
    3. Google APIS

* **Buat environment variable PATH untuk Java JDK dan Android SDK.**
Setelah proses install jdk selesai, langkah selanjutnya adalah buat environment variabel PATH untuk Java SDK.

    Windows → Search → System → Advanced System Settings → Environment variables → New

    ![Image](https://image.prntscr.com/image/EbkNdXnhTvC53_ac-OIarQ.png)

* **Buat Android Virtual Device**
Untuk menjalankan React Native perlu namanya Android Device, bisa dengan Geny Motion atau dari Android Studionya atau di Running di Device. 

Jika di Running di Device dan di Android Studio tidak bisa saya sarankan untuk menggunakan [GenyMotion](https://www.genymotion.com), Tinggal unsuh emulator yang versi 6.0 dan setting Path SDK di setinggan ADB Geny Motion.

Untuk First Project dengan RN (React Native) akan dibahas diartikel selanjutnya.