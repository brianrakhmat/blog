---
title: Tinggalkan Blogger, dan Saatnya beralih ke Jekyll yang lebih powerfull
date: 2017-10-08 20:27:00 +0000
categories:
- programming
tags:
- Jekyll
- Blog
- Github Pages
- Github
layout: single
excerpt: Kenapa alasan saya saat ini menggunakan Jekyll untuk menulis Blog, karena
  Jekyll lebih ringan, lebih cepat karena ga perlu ngeload database dan tampilannya
  juga dapat kita sesuaikan dengan semau kita dan tentunya Gratis tanpa perlu repot-repot
  mikirin bayaran tagihan hostingan. :D
image: assets/images/posts/jekyll.png

---
Kenapa alasan saya saat ini menggunakan Jekyll untuk menulis Blog, karena Jekyll lebih ringan, lebih cepat karena ga perlu ngeload database dan tampilannya juga dapat kita sesuaikan dengan semau kita dan tentunya Gratis tanpa perlu repot-repot mikirin bayaran tagihan hostingan. :D

Blog make Jekyll di Github Pages ini lebih baik ketimbang make Blogger karena dapat kita sesuaikan apalagi dengan tampilannya Blog di layar HP sangan tidak menarik untuk dibaca. Selain itu saya juga pernah make Wordpress Self-Hosting tapi sayang servernya sering down dan juga domain dan hostingya habis jadi saya putuskan make Github Pages aja buat blogging :D

Oke mari kita buat, saya asumsikan kita sudah buat yang namanya **Github Pages** biasanya nanti nama repoitorynya adalah _username.github.io_ , jika belum buat Github Pages silakan search artikel membuat Github Pages.

## Mulai
1. Cari template Jekyll untuk Github Pages di Google banyak tersedia, saya ambil contoh dari web [http://jekyllthemes.org/](http://jekyllthemes.org/)

2. Download Tema dan Ekstrak 

**Secara umum Struktur Folder Jekyll**
* _includes
* _layouts
* _posts
* _sass
* index.html
* _config.yml

3. Edit File **_config.yml** dan sesuaikan isinya. 
Contoh dari https://github.com/chesterhow/tale

<script src="https://gist.github.com/brianrakhmat/39ee28e1ebe31f5829986e5eba80026b.js"></script>

4. Jika sudah langkah selanjutnya push ke github jekyll ini dan Blogmu udah siap :D
![Image](https://image.prntscr.com/image/L70m5RZIQkav94T-eS3o9w.png)

Untuk nambah artikel / delete artikel semuanya make cmd jadi git add, git commit, dstnya karena jekyll ini statis jadi tidak menggunakan website, untuk penulisan artikelnya menggunakan format penulisan markdown (.md)...

Biar menambah kesan dinamis bisa ditambahkan plugins estimated reader, post automatic, sharer, analytics, dll seperti halnya web biasa.

Oh iya yang punya wordpress/blog bisa dimigrasi ke Jekyll dengan cara otomatis atau manual, selengkapnya googling aja ya :))