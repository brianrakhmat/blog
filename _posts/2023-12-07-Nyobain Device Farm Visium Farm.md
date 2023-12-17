---
title: Nyobain "Visium Farm", Device Farm paling worth it diantara lainnya, Bisa On-Prem juga!
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- Device Farm
- Device Farm Visium Farm
- Device Farm Visium
- Visium Farm
- Automation Test
- Appium
- Katalon Studio Community
- Katalon Remote Engine
- Katalon TestOps
- Jenkins
- Github
layout: single

header:
  image: "uploads/3c5b6308ddf24397a57646d074b51ee6.png"
  og_image: "uploads/3c5b6308ddf24397a57646d074b51ee6.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: Visium Farm adalah sebuah platform Device Farm yang menyediakan solusi untuk Automation / Manual Testing pada Real Device, bisa diimplementasikan on-premise dan cloud, support Android dan iOS juga dengan harga terjangkau dibanding kompetitor lainnya!

---

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701935757/public/eoxdqhcargqeeecycoor.png)

## **Overview Visium Farm**

Visium Farm adalah sebuah platform Device Farm yang menyediakan solusi untuk Automation / Manual Testing pada Real Device, visium farm juga support Android dan iOS, serta bisa diimplementasikan on-premise dan cloud,  sehingga cocok untuk penggunaan bagi company yang memilki regulasi tertentu yang mengharuskan data dan aplikasi hanya boleh di akses di Data Center, selain itu juga dari sisi harga bisa dibilang terjangkau dibanding kompetitor lainnya.

Untuk implementasi Visium Farm di On-Premise perlu menyiapkan beberapa server fisik yang berfungsi sebagai client yang connect ke Device, dan juga beberapa VM sebagai Main Engine.

Visium Farm juga compatible dengan Katalon sehingga jika sebelumnya kamu sudah memiliki ratusan test script di Katalon tinggal mengintegrasikan Appium Capabilites ke link url Visium Farm, Selain Katalon Visium juga memiliki product serupa untuk menuliskan Test Script seperti di Katalon namun dengan solusi yang terpisah dari Device Farm nya itu sendiri.

Visium Farm juga compatible dengan Jenkins atau product CI/CD lainnya karena terdapat API yang dapat melakukan Installasi APK / IPA ke seluruh Device, sehingga proccess installasi APL menjadi mudah, dan ya tentu saja dapat menjalankan automation testing dari Jenkins juga.

## **Architecture Visium Farm**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701936093/public/wemcuzyzddlmbowfvctt.png)


## **Feature Visium Farm**

Feature yang ditawarkan Visium Farm:
- Support Deployment / Installation APK/IPA to All Devices
- Automation Testing
- Manual Testing
- Remote Debugging Android dan iOS
- Support Rest API
- Capture Screenshot / Screen Recording during Testing
- Capture Network
- Device Logs
- Appium Logs
- Share Link Device
- dll

Selain fitur basic yang disebutkan diatas, Visium Farm juga memiliki feature unik yang tidak dapat ditemukan di product lainnya yaitu "Share Link", sehingga 1 device bisa di share ke tester / developer lainnya, hal ini memudahkan untuk memantau untuk troubleshooting/ debugging bareng-bareng.


Berikut beberapa screenshot dari Visium Farm:

**1. Menu Device List**

Di menu ini kita dapat melihat Device apa saja yang terkoneksi di Visium Farm, termasuk dapat melakukan Manual Testing, Automation configuration dan Lihat Koneksi untuk Remote Debugging.

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701936702/public/c5nyxcdnuvk7czijnvpc.png)

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937515/public/sqwhmpafmtf14dflicau.png)

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937533/public/lu3iawfq7bx45dwpi4uv.png)


**2. Menu Test Session**

Di halaman ini menampilkan data hasil testing Manual atau Automation, hasil Screen record vidio, Device Log dan Appium Log nya dapat di download

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701936788/public/glrpunk4szz8g8vhcakb.png)

**3. Menu Library**

Di halaman ini untuk mengupload APK / IPA ke Library nya Visium Farm, sehingga kalau kamu sebelumnya sudah memiliki APK / IPA di Laptop local kamu bisa uploadnya disini.

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937001/public/nt9ddrvsg2rstixaa7xw.png)

**4. Menu Deployment**

Di halaman ini kamu bisa menginstall APK / IPA yang sebelumnya kamu sudah upload ke Visium Library, untuk selanjutnya di install ke seluruh Device HP baik Android / iOS.

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937119/public/ho3lenqvjv9uo2wo59gr.png)

**5. Menu Report**

DI halaan ini kamu bisa melihat report penggunaan device, session, dll (bukan report testing pass / fail ya!)

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937280/public/n9noh0eycditbfiztavv.png)
![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937298/public/gvqzdifhgdgj1dbec2sj.png)
![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1701937308/public/b6tioj7nfkynyp1mp7oh.png)

Feature lainnya, adalah Remote Debugging, sehingga kamu bisa mengakses device kamu dan menggunakannya di Intellij IDEA / Android Studio dan Swift untuk melakukan debugging.

Untuk soal harga, Visium Farm menawarkan skema pricing yang berbeda dibanding kebanyakan kompetitor lainnya menggunakan skema pricing per device, namun Visium Farm menggunakan skema pricing berdasarkan Concurrent user yang akses, artinya 1 orang yang akses ke device maka dihitung 1 license, dan ketika tidak ada orang yang akses ke device maka license itu menjadi free kembali (intinya adalah license dihitung berdasarkan yang akses ke device baik manual atau automation), adapun jumlah device yang dapat connect ke visium farm bisa tidak terbatas tergantung jumlah port usb aja.

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih