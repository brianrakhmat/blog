---
title: Cara Sizing Jumlah Shard Redis yang dibutuhkan
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- Redis
layout: single

header:
  image: "uploads/redis-sizing-thumbnail.png"
  og_image: "uploads/redis-sizing-thumbnail.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: Kali ini saya akan sharing bagaimana caranya menghitung sizing Shard Redis yang dibutuhkan.
---

Hallo gimana kabarnya, semoga sehat selalu ya!,

Kali ini saya akan sharing gimana caranya untuk menghitung sizing Redis yang di fungsikan sebagai Caching dengan configurasi Active - Active DB (kalau di redis sebutannya adalah CRDB yang merupakan singkatan dari Conflict-free Replicated Database).

Redis sendiri dapat difungsikan dengan Active - Active dan Active Standby, yang dimana karena ini adalah Redis dia menyimpan datanya di Memory sehingga sizing yang di mainkan didalam nya akan kita bahas.

Berikut Best Praticesnya:
1. Jika kamu menggunakan redis CRDB maka 1 shard dapat menghandle 17.500 ops/second
2. Jika kamu menggunakan redis tidak CRDB alias Active - Standby maka 1 shard nya dapat menghandle hingga 25.000 ops/second

Kita akan coba bahas dulu bagaimana caranya:

1. Pastikan kamu sudah memiliki based line data, misalnya kamu sudah membuat DB Redis dan melakukan hit Performance Test misal hinggal 1000 concurrent users menggunakan tools seperti JMETER.
2. Catat resultnya yang ada pada Dashboard Redis. Ingat kamu harus selalu memantau dashboard redis ketika kamu running, karena Redis tidak bisa melihat history sebelumnya, kalaupun ada datanya akan di aggregate sehingga tidak bisa mencerminkan ketika posisi pada saat running.

Contoh:
Saya melakukan Performance Test pada aplikasi saya menggunakan tools JMeter dengan 1000 concurrent users, berikut result di dashboard redis

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/yplghrk4jrp3zva3drjb.png)

Pada saat pengetesan tersebut saya mendapatkan nilai max 10.111 ops/seconds dan angka ini akan dijadikan based line untuk menghitung jumlah shards yang dibutuhkan untuk dapat menghandle 10.000 concurrent users.

Mari kita buat table extra polasinya.

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/ggi1csayhqnqabriz9f4.png)

Dari table diatas ini untuk menghandle 10.000 concurrent user ternyata membutuhkan 101.110 ops/second dimana jumlah shardsnya adalah 101.110 / 17.500 = 6 shards Master dan 6 shards Slave sehingga in total kamu perlu 12 shards redis per Data Center.

Setelah didapatkan tadi, artinya jumlah tersebut adalah jumlah License yang diperlukan juga untuk dapat menghandle ops/seconds tadi, berarti kalau ada 2 DC (12 shards x 2 DC = 24 Shards License), Sehingga kamu butuh 24 shards license redis untuk 2 DC.

Note: Asumsi diatas adalah perhitungan untuk CRDB sehingga nilai ops/sec untuk 1 shardsnya adalah 17.500 , tetapi jika Active-Standby pembaginya adalah 25.000 ops/secons per shards.

Lalu bagaimana dengan specs hardwarenya? Mengacu pada link ini [https://docs.redis.com/latest/rs/installing-upgrading/install/plan-deployment/hardware-requirements/](https://docs.redis.com/latest/rs/installing-upgrading/install/plan-deployment/hardware-requirements/), 

Maka kita buat seperti ini:

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/la3k2df1zgerxm6vrp4o.png)

Nah, bagaimana sudah ngerti kaan cara menghitung shard Redis? Kalau belum berikut excelnya yang mungkin dapat membantu kamu untuk menghitung Redis.

[https://brii.my.id/calcredis](https://brii.my.id/calcredis)


Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih