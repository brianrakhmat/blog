---
title:  AI Code Assistant Codeium Enterprise On Premise
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- AI Coding Assistants
- Codeium
layout: single

header:
  image: "uploads/90bdafbccb354cd2a3c472049e7c318d.png"
  og_image: "uploads/90bdafbccb354cd2a3c472049e7c318d.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: Codeium adalah sebuah AI Coding Assistant yang dapat membantu kamu dalam  code generation, code completion, code refactoring, create unit test, code comment generation (explanation), dan lainnya. Codeium juga dapat di implementasikan di On Premise.

---

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/eopvwmgffjjvu9rvep8p.png)

## **Overview Codeium**

Pada artikel sebelumnya kita sudah membahas tools-tools AI apa saja yang dapat membantu kamu dalam melakukan coding, pada artikel kali ini saya akan lebih deep membahas satu tools AI yang namanya "Codeium", tools ini dapat implementasikan On Premise sehingga bisa lebih private, sebelum lebih lanjut ke hal teknis nya mari kita bahas dulu apa itu Codeium.

Codeium adalah sebuah AI Coding Assistant yang dapat membantu kamu dalam  code generation, code completion, code refactoring, create unit test, code comment generation (explanation), dan lainnya.

Codeium sendiri ada 2 versi yaitu versi Gratis dan Berbayar, untuk berbayar bisa di Cloud dan khusus versi yang Enterprise kita bisa implementasikan di On Premise. Pada Codeium Enterprise mereka menawarkan fitur tambahan yaitu learning dari SCM (Source Code Management) seperti Bitbucket / Github / Gitlab dimana AI nya Codeium akan melakukan "belajar" dari SCM nya kita, sehingga diharapkan apa yang menjadi suggestion / generation code akan lebih valid dengan kebutuhan company.

Untuk secara penggunaan di IDE mereka ada 2 versi plugin / extension, ada versi yang (free dan berbayar) dan ada versi yang enterprise. Untuk Versi Enterprise kita perlu memasukan credential server on prem kita yang sudah terinstall codeium.

## **Codeium Enterprise Additional Features**

**Personalization:**
1. None of data will leave your management and no-one will gain temporary or permanent access, including Codeium team.
2. Personalization on data from any Source Code Management (SCM) tool, such as Github, Gitlab, Bitbucket, etc, as well as non-code data that would be relevant for software development (ex. Confluence documentation).
3. Every user can get their own personalized system that also learns from their personal user behavior for maximizing productivity gains.
4. Codeium can run multiple personalized systems (each exposed to different subsets of your repository or repositories) on the same hardware resource.
5. Personalization will happen for Autocomplete, Chat, and any future capabilities. 

**Usage Analytics:**

Provide custom dashboards to both the enterprise and individual developers on Codeium use and related analytics, such as time saved.

## **Architecture Codeium Enterprise**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/krwveuqzxpkbk7fqksgk.png)

**System Deploy / Update (Purple)**

1. Installation and updates will happen via a single docker-compose provided by Codeium.
2. All dependencies like models and images will be fetched from Codeium’s container registry and storage buckets, or manual download.
3. Generate a DNS record that points from an internal address to the API server IP address, so that users can access Codeium within private network.
4. Installation (~2-4hrs), Configuration (~10min for base, ~3hrs for personalization)

**Codeium Execution (Blue)**
1. A user install the Codeium extension on any  IDEs, and setting the FQDN API server address . The extension will collect the context required by Codeium and send it with some user metadata to the API server.
2. The API server first verifies the user is authenticated via the PostgresDB.
3. The API server sends the context to a model controller layer.
4. This controller layer manages multiple “model runners” and intelligently distributes inference requests among them - once it identifies the runner, it will send the context over.
5. The model runner will use the GPU to generate the suggestions.
6. These suggestions are then propagated all the way back to the user’s extension. Both completion metadata (languages, length of completions, etc) and metadata about whether the user accepts or rejects a suggestion are logged in the PostgresDB.
7. Extension-clients will have to go through an additional remote language server.

## **Dashboard Monitoring**

Di dashboard ini kita bisa melihat analytics productivity penggunaan AI Codeium ini

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/fwdk7qq8mmpeufxi4f66.png)

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/zawushq8ey97bkf0zsjs.png)

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/py2zjjzxet2oexhxozfv.png)


Untuk instalasi Codeium di On Premise cukup mudah yaitu siapkan server fisik yang sudah terpasang GPU (Rekomendasinya RTX A5000) GPU diperlukan untuk proccessing learningnya, selain itu install Docker dan Docker Compose, karena Codeium sudah ada image dockernya kita hanya perlu run Docker Compose saja dan taraaaaaaa selamat anda sudah berhasil menginstall Codeium Enterprise on premise.

**Conclussion**

Tools AI Codeium ini sangat bermanfaat untuk meningkatan productivity, dan meningkatkan akselerasi bagi Developer Junior di tempat company bekerja, sehingga target task lebih cepat selesai. 

Tinggal pilih saja mau yang free ataupun yang versi berbayar, tergantung kebutuhan company masing-masing.

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih