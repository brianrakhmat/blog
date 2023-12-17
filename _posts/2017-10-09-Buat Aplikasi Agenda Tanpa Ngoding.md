---
title: Buat Aplikasi Agenda Tanpa Ngoding
date: 2017-10-09 16:50:39 +0000
categories:
- blog
- programming
tags:
- Android
- Bluemix
layout: single
excerpt: Disini saya akan membuat aplikasi agenda, aplikasi ini nantinya bisa berjalan
  di atas Android atau iOS, aplikasi ini berguna buat kamu yang punya banyak kesibukan,
  sehingga perlu mencatat agenda apa saja yang kamu akan lakukan, seperti bertemu
  teman, mengerjakan tugas, dll. aplikasi ini saya buat dengan bluemix, tanpa coding,
  cuman perlu waktu 15 menit buat aplikasi ini.
image: assets/images/posts/bluemixx.jpg

---
## Penjelasan
Disini saya akan membuat aplikasi agenda, aplikasi ini nantinya bisa berjalan di atas Android atau iOS, aplikasi ini berguna buat kamu yang punya banyak kesibukan, sehingga perlu mencatat agenda apa saja yang kamu akan lakukan, seperti bertemu teman, mengerjakan tugas, dll. aplikasi ini saya buat dengan bluemix, tanpa coding, cuman perlu waktu 15 menit buat aplikasi ini.

**Oke langsung saja ikuti tutorialnya**

1. Buat akun Bluemix di  [http://bluemix.net/](http://bluemix.net/) lalu klik signup
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_84.png)

2. Konfirmasi Email
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_85.png)

3. Isi seperti dibawah ini
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_89.png)


    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_90.png)

4. Setalah selesai, kamu aka melihat dashboard dan klik **Create App**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_91.png)

5. Pilih **Data Analytics -> Cloudant NoSQL DB**, seperti gambar dibawah ini
	![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_92.png)

6. Isi Service Name **"Agenda DB"**
	![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_94.png)

7. Lalu klik **Launch** ini untuk membuat Databasenya
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_95.png)

8. Setelah muncul, pilih **Database -> Create Database**.
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_96.png)

9. Setelah Create Database, pilih menu Design Documents, dan pilih **New Docs**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_98.png)

10. Buat Databasenya, jika sudah klik tombol **Create Document**, seperti contoh dibawah ini:
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_99.png)

11. Setelah Create Document, muncul halaman seperti ini
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_100.png)

12. lalu balik lagi ke laman Dashboard Bluemix, lalu pilih  **Apps - Mobile**, seperti gambar dibawah ini
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_101.png)

13. Create Project
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_103.png)

14. Pilih **Blank Project** dan isikan Project Name "Agendaku"
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_104.png)

15. Lalu pilih menu  **UI Builder dan Create New**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_106.png)
    
16. Pilih **LIST** dan Beri Nama  **"Agenda"**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_108.png)

17. Setelah itu Klik  **Data -> New Data Source**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_109.png)

18. **Add New Data Source -> Cloudant Config**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_111.png)

19. lalu kembali lagi ke service Agenda, lalu pilih Tab  **Service Credentials dan View**
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_113.png)

20. Dan akan terlihat seperti ini, ini untuk di isi pada Cloudant Config
    ![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_115.png)

21. lalu kembali lagi ke pengaturan Cloudant Config di Data, isi username, password, dan Host. Untuk Host ditambah "/nama_database. seperti gambar dibawah ini
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_116.png)

22. Jika berhasil muncul laman seperti ini, lalu kita balik lagi ke laman  **Screen**
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_118.png)

23. Ubah Data Source dari None ke Agenda_DB, lalu ubah tata layout seperti dibawah ini.
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_119.png)

24. Lalu Back dan Klik Push Notification lalu Create
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_123.png)

25. Buat Service Name dengan nama "Agenda Push" lalu klik Configure Now
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_125.png)

26. Buka tab baru klik [https://firebase.google.com](https://firebase.google.com) lalu klik Go to console, Buat proyek baru
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_127.png)

27. Setelah Create, lalu klik tombol Gear dan pilih Setelan Proyek  

28. Pilih  **Cloud Messaging**, catat API dan Sender ID
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_130.png)

29. Kembali lagi ke **Push Notification -> Configure**, isi dengan API dan Sender ID dari Firebase Google
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_131.png)

30. Setelah itu pilih menu Send Notification, apabila Error No Devices Found berarti sudah jalan
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_133.png)

31. Setelah itu kita tambahkan fitur Analytics, pilih icon Grafik dibawah Push Notificaion
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_135.png)

32. Kembali lagi ke Project Kita tadi, lalu pilih UI Builder
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_138.png)

33. lalu pilih Setting, ganti Icon, Collor, dll.
![Image](https://brianrakhmat.github.io/assets/images/posts/bluemix/Screenshot_142.png)

34. Jika sudah lalu back, dan pilih **Code** dan pilih device Android dan klik Download APK
35. Terakhir, install pada Device Android kamu

**Fork Me on [Github](https://github.com/brianetlab/Agendaku)**