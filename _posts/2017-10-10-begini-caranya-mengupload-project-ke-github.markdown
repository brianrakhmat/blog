---
title: Begini Caranya Mengupload Project Ke Github
date: 2017-10-10 08:54:00 +0000
categories:
- blog
tags:
- Github
- Uploads
- Cara Upload Github
excerpt: Git adalah tempat untuk mendokumentasikan project, kamu juga bisa bekerja
  secara bersamaan jadi project kamu bisa cepat selesai walaupun satu tim saling berjauhan.
image: "/uploads/github.png"

---
**Dasar Git**
Jadi, sebenarnya apa yang dimaksud dengan Git? Ini adalah bagian penting untuk dipahami, karena jika anda memahami apa itu Git dan cara kerjanya, maka dapat dipastikan anda dapat menggunakan Git secara efektif dengan mudah. Selama mempelajari Git, cobalah untuk melupakan VCS lain yang mungkin telah anda kenal sebelumnya, misalnya Subversion dan Perforce. Git sangat berbeda dengan sistem-sistem tersebut dalam hal menyimpan dan memperlakukan informasi yang digunakan, walaupun antar-muka penggunanya hampir mirip. Dengan memahami perbedaan tersebut diharapkan dapat membantu anda menghindari kebingungan saat menggunakan Git.

Bahasa Sederhananya, tempat untuk mendokumentasikan project, kamu juga bisa bekerja secara bersamaan jadi project kamu bisa cepat selesai walaupun satu tim saling berjauhan.

**Langsung saja pada tutorialnya:**

1. Buat akun pada [https://github.com/](https://github.com/)

2. Setelah selesai, lalu download Git, download disini [https://git-scm.com/downloads](https://git-scm.com/downloads)

3. Instal seperti biasa

4. Lalu login ke akun github dan buat repository baru, klik link [https://github.com/new](https://github.com/new)
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_62.png?alt=media&token=e5df5fe7-3970-4f10-b806-5362023447d7)
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_63.png?alt=media&token=6a9bdb14-291f-41d1-bf91-aee77fed511e)
lakukan seperti gambar diatas: Repository name: (Diisi nama repositorya) Desciption: (Diisi deskripsi repositorynya (tidak wajib)) lalu set Public, Private, default Public, lalu klik tombol berwarna hijau **Create Repository.**

5. Setelah Create Repository muncul halaman seperti ini:\
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_64.png?alt=media&token=c3f99959-af64-4ba3-9721-da043f038aab)
ini berfungsi sebagai perintah command line\\

6. Setelah itu buka project yang akan dimasukkan ke Github, caranya klik kanan pada folder project dan pilih ***Git Bash Here***
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_65.png?alt=media&token=e5744638-784d-45a3-af9a-058f99608ed7)
dan muncul command line
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_66.png?alt=media&token=9f773568-ec29-442a-893b-4c5839b0baf9)

7. Ketikkan perintah seperti di step 5:
```
echo "# Repository-Baru" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/brianetlab/Repository-Baru.git
git push -u origin master
```
Penjelasan: 
* git add = untuk memiliih file yang akan dimasukan ke github (kalau pilih semua: " git add . " ) 
* git commit = untuk memberi commit/pesan git remote = alamat untuk memasukan ke github 
* git push = untuk ngepush semuanya ke github klik enter dan lihat project kamu sudah terupload ke Github

8. Selamat Project kamu sudah masuk ke Github!
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_68.png?alt=media&token=c012cace-d752-4c53-bc6d-6415ab8471b9)

Selesai sekarang kamu bisa mendokumentasikan project kamu!