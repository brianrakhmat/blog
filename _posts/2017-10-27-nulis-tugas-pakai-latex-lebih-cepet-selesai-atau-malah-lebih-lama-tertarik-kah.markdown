---
title: Nulis Tugas Pakai LaTex, Lebih cepet selesai atau malah lebih lama? Tertarik
  kah?
date: 2017-10-27 09:44:00 +0000
categories:
- blog
tags:
- Cara Menulis Menggunakan LaTex
- LaTex
excerpt: Jadi hari ini saya barusan mendapat pelatihan penulisan menggunakan LaTex
  dari Prodi, modulnya dari Departemen Matematika Fakultas MIPA UGM, yang saya pahami
  LaTex itu cara menulis melalui text editor dengan syntax-syntax tertentu agar bisa
  dicompile. Hasil Compile-annya menghasilkan output .pdf.
image: "/uploads/Latex.png"

---
jadi hari ini saya barusan mendapat pelatihan penulisan menggunakan LaTex dari Prodi, modulnya dari Departemen Matematika Fakultas MIPA UGM, yang saya pahami LaTex itu cara menulis melalui text editor dengan syntax-syntax tertentu agar bisa dicompile. Hasil Compile-annya menghasilkan output .pdf.

Menurut Sejarahnya LaTex itu berasal dari kata La dan Tex, Tex yaitu suatu programming language yang diciptakan khusus untuk  sistem pengetikan  (typesetting system) yang akan menghasilkan dokumen
\(teks, gambar, notasi matematis) berkualitas tinggi. TEX diciptakan oleh Prof. Donald Knuth sekitar tahun 1978. Dan kata La sepertinya dari nama peniciptanya yakni Leslie Lamport pada tahun 1985. Dari situ terciptanya LaTex yang merupakan user interface dari Tex, ia menciptakan LaTex untuk mengotomatisasi semua perintah umum dan untuk menyiapkan sebuah
dokumen.

**Tools yang diperlukan**

1. Instal [MikTex](http://miktex.org/)

2. Text Editor WinEdt

3. Document Viewer (PDF Reader)

**Cara Menulis**
Jadi cara menulsnya, tuliskan documentclassya dibawah ini:

    \documentclass{article}
    \begin{document}
       
       isi filenya...........
    
    \end{document}

Contohnya gini kita akan menuliskan huruf tebal, miring dll

**Text Normal**

    \textnormal{Text Normal}

Outputnya:
![Image](https://image.prntscr.com/image/uw3rjZ9zQBqB6bcx96LJ2Q.png)

**Miring**

    \emph{Text Miring}

Outputnya:
![Image](https://image.prntscr.com/image/_IGRnhCESiyemv_FOcgQNA.png)

**Font Times New Roman**

    \textrm{times new roman}

Outputnya:
![Image](https://image.prntscr.com/image/AKwPszEVQ6eeRSHd-x2i0Q.png)

**Font Sans Serif**

    \textsf{serif}

Outputnya:
![Image](https://image.prntscr.com/image/9W7WrOHGQIe_h78-8Hc7FA.png)

**Cetak Tebal**

    \textbf{Bold}

Outputnya:
![Image](https://image.prntscr.com/image/AaS_23SbRomxnTKFbUptEQ.png)

**Penulisan Matematika**

    \documentclass{article}
    \begin{document}
    Rumus untuk mencari akar-akar persamaan kuadrat $ax^(2)+bx+c=0$;
    $$x_{1,2}=\frac{-b\pm\sqrt{b^{2}-4ac}}{2a}.$$
    \end{document} 

Outputnya:
![Image](https://image.prntscr.com/image/iq0e-XPVTmOcaf3Pa2l21g.png)

Ohiya buat kamu yang mau tau modul ini silakan download dibawah ini, login menggunakan akun (Uin Suka) dulu yaa..
[Download Modul Pelatihan LaTex, Template Skripsi, Template Jurnal](http://s.id/IB5)

Gimana keren bukan dari yang text editor biasa tau2nya pas dicompile jadi sebuah dokumen pdf yang memunculkan fungsi2 matematis, apakah kamu tertarik menggunakan LaTex? Apakah pengerjaan penulisanmu lebih cepat atau bahkan lebih lambat? Itu tergantung pilihan kamu yaa! :D