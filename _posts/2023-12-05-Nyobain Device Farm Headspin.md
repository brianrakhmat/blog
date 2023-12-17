---
title: Nyobain Device Farm Headspin
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- Device Farm
- Headspin
- Automation Test
- Appium
- Katalon Studio Community
- Katalon Remote Engine
- Katalon TestOps
- Jenkins
- Github
layout: single

header:
  image: "uploads/d09fa9eab7f64344a533f6ebf584ab37.png"
  og_image: "uploads/d09fa9eab7f64344a533f6ebf584ab37.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: Headspin adalah sebuah platform Device Farm yang menyediakan solusi untuk Automation / Manual Testing pada Real Device maupun Virtual Device baik aplikasi Android maupun iOS dan platform lain seperti Smart TV, Smart Watch dll.

---

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702098032/apuvm0lz5jjufqjrliey.png)

## **Overview Headspin**

Headspin adalah sebuah platform Device Farm yang menyediakan solusi untuk Automation / Manual Testing pada Real Device maupun Virtual Device baik aplikasi Android maupun iOS dan platform lain seperti Smart TV, Smart Watch dll yang dapat di implementasikan di Cloud dan on-premise, sehingga cocok untuk penggunaan bagi company yang memilki regulasi tertentu yang mengharuskan data dan aplikasi hanya boleh di akses di Data Center.

Untuk implementasi On-Premise mereka provide Appliance Box yang didalamnya sudah include dengan Mac Mini dan software nya sehingga tinggal plugin Mobile Device dan Connect ke Network.

Headspin juga kompatible dengan Katalon sehingga jika sebelumnya kamu sudah memeliki test script di Katalon tinggal mengintegrasikan Appium Capabilites ke link url Headspin


![Image](https://api-dev.headspin.io/v0/private/onprem/pbox-rack-installation/overview-perspective.png)

## **Architecture Headspin**

![Image](https://api-dev.headspin.io/v0/private/onprem/onprem-architecture/isolatednet.png)


## **Feature Headspin**

Feature yang ditawarkan Headspin:
- Automation Testing
- Manual Testing
- Remote Debugging Android dan iOS
- Testing Report
- dll

Selain fitur basic yang disebutkan diatas, Headspin juga support Biometrics seperti Fingerprint / Face ID dengan mengintegrasikan Headspin SDK pada Aplikasi yang akan di Testing. Fitur ini bisa dibilang juga sebagai fitur unggulan dibanding kompetitor lain karena tidak semuanya product Device Farm support Integrasi dengan Hardware. (Namun sepertinya belum bisa support NFC)

Berikut beberapa screenshot dari Headspin:

**1. Menu Remote Control**

Di menu ini kita dapat melihat Device apa saja yang terkoneksi di Headspin, termasuk dapat melakukan Manual Testing, Automation configuration dan Lihat Koneksi untuk Remote Debugging.

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702098107/osytkx41cf85lrifchkm.png)
![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702098187/buxbfxbfimhhiytp8rky.png)
![Image](http://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702098187/public/lmkmxalnfoa56cpf9jrx.png)
![Image](http://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702098187/public/lrrvz3k6g4ozbl60sfvp.png)

**2. Menu Performance**

Di halaman ini menampilkan data hasil Performance dari sisi hardware device baik testing Manual dan atau Automation

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701751924/public/ff7dpn3blp47bf8uikkm.png)
![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701752245/public/nchhtdkanzi7t9u2fn2f.png)
![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701752284/public/x0n6kbycjeujl1whbcvo.png)

**3. Menu Grafana Report**

Di halaman ini menampilkan data testing report seperti Pass / Failed

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701752532/public/rngoswpulppjzgvvtfdk.png)
![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701752631/public/swxjqyvstuidf01odtrg.png)
![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701752717/public/twiyjdsv7rx7lcbmngfm.png)

**3. Menu Usage Report**

Di halaman ini menampilkan data usage dari penggunakan device farm

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701752834/public/ozb0qdigjfkpsmdoao5n.png)

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih