---
title: Membuat Fitur Search Pada Jekyll Dengan Lunr.js
date: 2017-10-18 06:46:00 +0000
categories:
- blog
- programming
tags:
- search
- lunr.js
excerpt: Lunr.js adalah javascript untuk membuat fitur pencarian pada web, ini juga
  dapat diimpelementasikan pada Jekyll
image: "/uploads/lunrjs-card.png"

---
## Apa Itu Lunr.js?
Lunr.js adalah javascript untuk membuat fitur pencarian pada web, ini juga dapat diimpelementasikan pada Jekyll

## Cara Membuat
1. Buat File **search.js** di folder assets/js
<script src="https://gist.github.com/brianrakhmat/f8b1fefa13ce50147d084fd68666d413.js"></script>

2. Buat File **lunr.min.js** di folder assets/js
<script src="https://gist.github.com/brianrakhmat/defedb0fabc4df617fe255caedf8eb88.js"></script>

3. Buat File **search.html** pada folder _layouts
<script src="https://gist.github.com/brianrakhmat/42b7502bc38270065e0612586bfe640e.js"></script>

4. Buat File **search.html** pada root project mu
<script src="https://gist.github.com/brianrakhmat/3d22367886036a1a2ee14bf07975b36d.js"></script>

Selamat telah berhasil menambahkan fitur search di Jekyll

![Image](https://image.prntscr.com/image/tE1doX3iTwiO8kf5710DJQ.png)