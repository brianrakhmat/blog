---
title: Cara Custom Domain Blogspot Menggunakan Sub Domain di CPanel
date: 2017-08-25 13:15:00 +0000
categories:
- programming
tags:
- Csutom Domain Blogspot
- Blogspot
- Domain
- CPanel
layout: single
excerpt: Disini saya akan membahas bagaimana caranya mengcustom/mengubah nama domain
  blogspot ke dalam nama sub domain pada cPanel, cara ini hampir mirip dengan mengcustom
  pada laman Client pada saat membeli Domain.
image: assets/images/posts/domain.png

---
Disini saya akan membahas bagaimana caranya mengcustom/mengubah nama domain blogspot ke dalam nama sub domain pada cPanel cara ini hampir mirip dengan mengcustom pada laman Client pada saat membeli Domain.

## Ayo langsung saja pada tutorialnya:

1. Buat Sub Domain pada cPanel, jika belum tau cara buat subdomain, silakan googling sendiri ^^

2. Pilih menu **Editor Zona Selanjutnya**
![Image](https://cdn-images-1.medium.com/max/800/1*kfArU_vnqAG6bOPchVvCwg.png)

3. Lalu pilih Domainnya, dan scroll kebawah untuk melihat **Record File Zona**
![Image](https://cdn-images-1.medium.com/max/800/1*znz0plxa--b80g8CvdkWbw.png)
![Image](https://cdn-images-1.medium.com/max/800/1*b1swLljS9qDVl2-TLI0rmQ.png)
(Tampilan Editor Zona Selanjutnya)

4. Selanjutnya buka Blogger Kamu, pilih menu Setelan dan klik “+ Siapkan URL pihak ke-3 untuk blog Anda — Mengarahkan URL terdaftar Anda ke blog Anda.”
![Image](https://cdn-images-1.medium.com/max/800/1*HdRrB7-saMUvjAXFkWSsIw.png)
![Image](https://cdn-images-1.medium.com/max/800/1*fR6eiiXedAdad0UqzaB-7A.png)
isi dengan nama SubDomain yang sebelumnya sudah dibuat di cPanel, lalu klik **simpan**

5. Jangan Khawatir apabila muncul kesalahan seperti ini, catat kode seperti ini
![Image](https://cdn-images-1.medium.com/max/800/1*svpW1RJ44jZzl1eS4ZWN2w.png)
Memasang Pada CPanel

6. Tambah Record
![Image](https://cdn-images-1.medium.com/max/800/1*r1RyFd0ElYYQNKm0LZvysg.png)
Tipe: CNAME 
Nama: blog
TTL: 14400
CNAME: ghs.google.com

7. Tambah Record Lagi
![Image](https://cdn-images-1.medium.com/max/800/1*XA1vggmqp5aV9W9CMABRrQ.png)
Tipe: CNAME
Nama: (Diisi Kode yang dari Blogger)
TTL: 14400
CNAME: (Diisi Kode yang dari Blogger)

8. Langkah selanjutnya kembali ke Blogger, dan klik kembali tombol **Simpan** seharusnya blognya sudah terarah dengan domain kamu.
![Image](https://cdn-images-1.medium.com/max/800/1*cpZ2iHWHIJ0_qdcTVsxnTw.png)

9. Cek Blog kamu apakah sudah terarah atau belum, jika belum berhasil silakan menunggu beberapa waktu biasanya tidak lama untuk masa propagansi, jika sampai 24 jam belum maka silakan ulangi step by stepnya
![Image](https://cdn-images-1.medium.com/max/800/1*WDvP2G5AtqYgKzmTE0FytA.png)

## Selesai! Semoga Bermanfaat! 🙂