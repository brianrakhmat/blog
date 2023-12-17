---
title: Cara Buat Kolom Komentar Disqus dengan Jekyll
date: 2017-10-09 03:27:00 +07:00
categories:
- programming
tags:
- Disqus
- Komentar
- Jekyll
layout: single
excerpt: Kali ini saya akan membahas bagaimana caranya membuat kolom komentar dengan
  Jekyll menggunakan Disqus. Cukup simple dan tidak perlu repot-repot memikirkan bagaimana
  databasenya, pokoknya instan deh.
image: assets/images/posts/disqus.png
---

Kali ini saya akan membahas bagaimana caranya membuat kolom komentar dengan Jekyll menggunakan Disqus. Cukup simple dan tidak perlu repot-repot memikirkan bagaimana databasenya, pokoknya instan deh. 
Oh iya saya asumsikan sudah buat akun Disqusnya, kalau belum bisa google cara buat akun Disqus ya... :D

## Mari Mulai
1. Edit **_config.yml_** , tambahkan ini:
<script src="https://gist.github.com/brianrakhmat/b1a40636eb18933d5daed7f9681d5616.js"></script>

2. Buat file **comment.html** di folder **_includes_**
<script src="https://gist.github.com/brianrakhmat/54dc64c602f0b72192bc5f6ebc223840.js"></script>

3. Buka file **post.html** di folder **_layouts_** tambahkan script dibawah ini diakhir content artikel atau lokasi yang ingin ditempatkan kolom komentar
<script src="https://gist.github.com/brianrakhmat/d655f482ff6c3dae48237412dd019333.js"></script>

## Selamat kamu berhasil membuat Disqus Comments di Jekyll :D
![Image](https://image.prntscr.com/image/LDmP_O4LRxmV6qyGuxAqZg.png)