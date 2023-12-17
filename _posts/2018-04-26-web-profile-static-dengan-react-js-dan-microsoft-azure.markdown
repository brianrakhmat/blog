---
title: Web Profile Static dengan React JS dan Microsoft Azure
date: 2018-04-26 12:58:00 +0000
categories:
- blog
tags:
- Azure Website
- React JS
header:
  image: "/uploads/Screenshot_187.png"
excerpt: Membuat Web Statis dengan React JS di Microsoft Azure

---
**Prerequirements:**

1. Instal NodeJS ([https://nodejs.org/en/download/](https://nodejs.org/en/download/))

2. Install Git CLI ([https://git-scm.com/downloads](https://git-scm.com/downloads))

3. Download folder images ([https://drive.google.com/open?id=1KSWUVVoH6Egkn46qqbqJx1ozb9Pht559](https://drive.google.com/open?id=1KSWUVVoH6Egkn46qqbqJx1ozb9Pht559))

**Rencana**

Kita akan membuat Project Web Profile menggunakan React JS dan Microsoft Azure

![Screenshot_166.png](/uploads/Screenshot_166.png)

**#1 Membuat Project React**

npm install -g create-react-app

create-react-app web-profile

**Coba Jalankan!**

cd web-profile

npm start

![Screenshot_188.png](/uploads/Screenshot_188.png)

**#2 Modifikasi Project**

![Screenshot_190.png](/uploads/Screenshot_190.png)

1\. Ekstrak dan masukan folder images yang sudah didownload tadi pada folder ***src.***

2\. Buat folder **components** didalam folder ***src***

3\. Buat **4** File (Welcome.js, NavBar.js, Project.js, Footer.js) di dalam folder **components** yang sudah kita buat tadi.

<script src="https://gist.github.com/brianrakhmat/9e6e73d0cddf2c02ed05dfe4b106a12a.js"></script>

4\. Modifikasi file **index.html** pada ***public/index.html***

<script src="https://gist.github.com/brianrakhmat/3cb0b401223d2a47c5445c60bbd64389.js"></script>

5\. Sekarang Build dan Jalankan!

npm run build

npm start

![Screenshot_189.png](/uploads/Screenshot_189.png)

**#3 Buat Akun Microsoft Azure**

1\. Login ke **portal.azure.com** menggunakan akun **microsoft / outlook**

![Screenshot_165.png](/uploads/Screenshot_165.png)

Menuju ke laman **view my bill**

![Screenshot_164.png](/uploads/Screenshot_164.png)

Langkah selanjutnya kita akan menambahkan **subscription **menggunakan akun email Kampus. Kunjungi laman: [https://azure.microsoft.com/en-us/offers/ms-azr-0144p/](https://azure.microsoft.com/en-us/offers/ms-azr-0144p/)  lalu klik **Activate**

![Screenshot_163.png](/uploads/Screenshot_163.png)

Pilih **School Email Adreess** dan masukan alamat email kampus

![azurestudent.png](/uploads/azurestudent.png)

Tunggu beberapa saat, email verifikasi akan dikirimkan ke email student mu.

![Screenshot_167.png](/uploads/Screenshot_167.png)

![Screenshot_168.png](/uploads/Screenshot_168.png)

![Screenshot_169.png](/uploads/Screenshot_169.png)

Selamat akun Azure kamu telah bisa digunakan!

**#3 Deploy Aplikasi ke Microsoft Azure**

1\. Ke laman **Create Resource **cari **Web App**

![Screenshot_170.png](/uploads/Screenshot_170.png)

Isikan sesuai dibawah ini:

![Screenshot_171.png](/uploads/Screenshot_171.png)

Go To Resource:

![Screenshot_172.png](/uploads/Screenshot_172.png)

2\. Deploy Projectan kita ke Microsoft Azure menggunakan Github

Create **New Repository **di Github

![Screenshot_173.png](/uploads/Screenshot_173.png)

![Screenshot_174.png](/uploads/Screenshot_174.png)

3\. Login ke halaman [https://www.visualstudio.com/](https://www.visualstudio.com/)  menggunakan akun microsoft kamu, lalu klik **Create New Account**

![Screenshot_175.png](/uploads/Screenshot_175.png)

![Screenshot_176.png](/uploads/Screenshot_176.png)

Go to **Build and Release **dan klik ikon  **\+** **New Definition**

![Screenshot_177.png](/uploads/Screenshot_177.png)

Pilih **Source **dari **Github **dan pilih project mana yang akan dideploy dan klik **Continue**

![Screenshot_178.png](/uploads/Screenshot_178.png)

Selanjutnya kita akan membuat  *otomasi *npm* *run build dengan cara select template **empty **dan **apply**

![Screenshot_179.png](/uploads/Screenshot_179.png)

langkah selanjutnya **add task **dan pilih **NPM**

![Screenshot_180.png](/uploads/Screenshot_180.png)

isikan sesuai dibawah ini:

![Screenshot_181.png](/uploads/Screenshot_181.png)

selanjutnya **add Task** dan pilih **NPM **lagi

edit **display name** menjadi **NPM Run Build **, **Command **menjadi **Custom, **dan **Command and arguments **diisi **run build**

![Screenshot_182.png](/uploads/Screenshot_182.png)

Tambahkan **Azure App Service Deploy **isikan sesuai dibawah ini, jangan lupa package or folder diganti dengan:

> $(System.DefaultWorkingDirectory)/build

![Screenshot_183.png](/uploads/Screenshot_183.png)

Selanjutnya klik **Save dan queque**

![Screenshot_184.png](/uploads/Screenshot_184.png)

Tunggu proses **Queue **sampai selesai

![Screenshot_185.png](/uploads/Screenshot_185.png)

Selamat Project anda sudah berhasil di Deploy ke Azure Website! 

Link URL: [https://profileku.azurewebsites.net/](https://profileku.azurewebsites.net/)

![Screenshot_186.png](/uploads/Screenshot_186.png)

Github Repo: [https://github.com/brianrakhmat/web-profile](https://github.com/brianrakhmat/web-profile)

**How To Start?**

1\. Clone Repo [https://github.com/brianrakhmat/web-profile.git](https://github.com/brianrakhmat/web-profile.git)

2\. cd web-profile

3\. npm install

4\. npm run build

5\. npm start

**Thankyou! :)**
