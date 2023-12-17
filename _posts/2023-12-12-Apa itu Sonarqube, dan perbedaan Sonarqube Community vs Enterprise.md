---
title: Apa itu Sonarqube, dan perbedaan Sonarqube Community vs Sonarqube Enterprise
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- Sonarqube
- Sonarqube Community
- Sonarqube Enterprise
layout: single

header:
  image: "uploads/9c9db9790dbf4ecba90c17c441f87037.png"
  og_image: "uploads/9c9db9790dbf4ecba90c17c441f87037.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: SonarQube adalah platform open-source yang digunakan untuk melakukan analisis source code. Tujuan utama dari SonarQube adalah untuk membantu tim developer untuk mengidentifikasi dan memperbaiki potensi problem dalam source code mereka, sehingga meningkatkan kualitas dari source code.

---

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/wwql1j2abj2sypoqmqzy.png)

## **Apa itu Sonarqube?**

SonarQube adalah platform open-source yang digunakan untuk melakukan analisis source code. Tujuan utama dari SonarQube adalah untuk membantu tim developer untuk mengidentifikasi dan memperbaiki potensi problem di source code mereka, sehingga meningkatkan kualitas dari source code itu sendiri.

## **Key features of SonarQube**

1. **Static Code Analysis**: SonarQube melakukan analisis statis terhadap source code untuk mengidentifikasi berbagai jenis issues, seperti bug, kode yang sulit dipahami (code smells / indications of more maintainable or readable code), celah keamanan (security vulnerabilities) dan role coding guideline.

2. **Monitoring and Reporting**: Sonarqube memberikan report yang detail tentang hasil analisis, yang memungkinkan tim developer untuk men-tracing issues dan memahami changes vode quality dari sebelum perbaikan dan setelah perbaikan. Intinya feature ini membantu devloper untuk fokus pada area yang perlu perbaikan / fixing.

3. **Integration with Development Tools**: SonarQube dapat di integrasikan dengan berbagai macam developer tools IDE (Intellij IDEA / VS Code / XCode dll) dan project management systems (Jira, dll).


4. **Code Quality Measurement**: SonarQube memberikan feature untuk mengukur code quality dan menampilkan grafik dari waktu ke waktu untuk melihat quality code apakah naik atau turun, jika quality code menurut perlu adanya perbaikan / improvement.

5. **Security Code Scanning**: Selain aspek kualitas kode, SonarQube juga dapat digunakan untuk mengidentifikasi potensi celah keamanan (security vulnerabilities) di source code. Ini membantu developer untuk memitigasi risiko keamanan yang mungkin muncul dalam aplikasi kita.

Nah sudah cukup mengerti kaan apa itu Sonarqube dan fitur-fiturnya, mari kita bahas topik selanjutnya yaitu Cara Scan Sonarqube.

## **Cara penggunaan Sonarqube**

Cara scan sonarqube sebetulnya mudah, kamu bisa import project dari SCM (Source Code Management) seperti Github / Bitbucket / Gitlab / dll, dan pilih scanner nya tergantung bahasa pemrograman yang digunakan, seperti Maven, Gradle, .NET, atau others (JS, TS, GO, PHP, Python, dll).

**Contoh Maven**
```
  mvn clean verify sonar:sonar \
    -Dsonar.projectKey=<Your Project Key> \
    -Dsonar.projectName='<Your Project Name>' \
    -Dsonar.host.url=<Your Domain URL Sonarqube>:<port> \
    -Dsonar.token=<Your Token>
```

Nah script diatas adalah contoh untuk scan sonarqube dengan Maven Spring boot, cara penggunannya mudah tinggal jalankan script diatas di terminal Intellij IDEA dan akan langsung jalan.

Jika berhasil, maka sonarqube akan menampilkan hasilnya apakah Pass / Failed, jika Failed, maka quality code kamu dinilai kurang oleh rules yang ada di Sonarqube, kamu juga bisa meng adjust nilai treshold rule sonarqube.

**Contoh Kondisi Failed**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/swceaencspkjec3vbe7d.png)

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/wmivvpaquilnbd0wcd2d.png)

**Contoh Kondisi Pass**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/v4rndnes3xlvn7enqss1.png)

Nah sudah cukup mengerti kan cara penggunaan sonarqube seperti apa, mari selanjutnya kita bahas perbandingan antara Sonarqube Community vs Sonarqube Enterprise.

## **Perbandingan Antara Sonarqube Community vs Sonarqube Enterprise**

**Language Comparation**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/bjzphy2xf2ylq35m5itt.png)

Dari sisi programming language, sonarqube enterprise memiliki jumlah yang lebih banyak secara total support **34 programming language** dibanding sonarqube community yang hanya memiliki **22 programming language**.

**Rules Comparation**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/ucrqgvnwrwwy33dshlyo.png)

**Security Category Comparation**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/augaklwq3ezqgqppyqkz.png)

**Conclussion**

Nah, kalau dilihat secara keseluruhan, perbandingan antara sonarqube community dan sonarqube enterprise tidak beda jauh, sehingga jika project kamu dirasa cukup untuk menggunakan versi community ya pilih aja community dan apabila jika ada budget lebih, kamu bisa pilih yang versi Enterprise, karena cost yang dikeluarkan untuk subscription sonarqube enterpise lumayan mahal sebesar **$20.000 1m/line of codes**.

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih