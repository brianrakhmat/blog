---
title: Cara Sizing Elasticsearch Hot, Warm dan Cold Node
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- ELK
- Elasticsearch
layout: single

header:
  image: "uploads/76ce2d95ea3f44f0b45ac7d0f0ec42b7.png"
  og_image: "uploads/76ce2d95ea3f44f0b45ac7d0f0ec42b7.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: Kali ini saya akan sharing gimana caranya untuk menghitung berapa jumlah node dan spec server yang dibutuhkan untuk membangun cluster Elasticsearch dengan Architecture hot, warm, dan cold node.
---

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/pohkd8fkvczmqekdheuc.png)

Hallo gimana kabarnya, semoga sehat selalu ya!,

Kali ini saya akan sharing gimana caranya untuk menghitung berapa jumlah node dan spec server yang dibutuhkan untuk membangun cluster Elasticsearch dengan Architecture hot, warm, dan cold node.

Untuk artikel ini saya asumsikan temen-temen sudah mengetahui apa itu **ELK (Elasticsearch, Logstash, dan Kibana)** beserta kegunaan dan cara kerjanya yaa.

Kalau belum saya sedikit share aja apa itu Elasticsearch, pada dasarnya elasticsearch merupakan database NoSQL yang berfungsi sebagai tempat menyimpan data, bisa berupa Logs, atau data yang sifatnya transactional.

## **Kapan Elastic dibutuhkan?**

1. **Saat perlu search Data**

● select * from alamat where jalan = ‘Jalan Sudirman Kav. 54-55’

● Select * from alamat where jalan = ‘%Jalan Sudirman%’

● Select * from alamat where jalan = ‘%Jl. Sudirman%’

Untuk mencari data seperti diatas sulit menggunakan database pada umumnya, maka daripada itu untuk mempermudah mencari data seperti diatas kita perlu menggunakan Elasticsearch.

2. **Saat perlu membuat Aggregate Data**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/peoysf4rp9gfkabmk3ge.png)

3. **Saat perlu membuat pencarian data yang complex**

● Autocomplete

● Ngram

● Sinonim

● dll

## **Architecture Elasticsearch**

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/xbkvqnfqoc7qtenw8aeu.png)

Oke sekarang sudah lebih paham kan apa itu Elasticsearch dan cara kerjanya secara High Level, lanjut kita bahas bagaimana cara sizing Elasticsearchnya.

Pada dasarnya Elasticsearch itu ada berbagai macam Nodes seperti Hot Nodes, Warm Nodes, dan Cold Nodes, tergantung bagaimana penggunaannya.

1. **Hot Nodes** = Hot nodes diperuntukan bagi data / index yang sering di update atau di query
2. **Warm Nodes** = Warm nodes diperuntukan bagi data / index yang tidak di update tapi ingin hanya di query 
3. **Cold Nodes** = Cold nodes diperuntukan bagi data / index yang tidak di update dan tidak sering di query, karena proses searchnya akan lebih lambat.

selain diatas ada juga **Frozen Nodes**, yang diperuntukan bagi data yang tidak di update dan jarang di query sehingga proses searchnya akan lebih lambat dari Cold Nodes, dimana biasanya ketika sudah masuk fase Frozen maka data akan di hapus atau dipindahkan ke S3 / Object Storage tergantung kebutuhan perusahaan.

Proses-proses diatas merupakan bagian dari ILM (Index Lifecycle Management) yang dimana itu semua dapat di configurasi di Kibananya berapa hari index / data tersebut ada di Hot Nodes, berapa hari ada di Warm Nodes, dan berapa hari ada di Cold Nodes hingga di Delete atau dipindahkan ke S3 / Object Storage.

## **Sizing Elasticsearch**

Sekarang mari kita bahas bagaimana cara menghitung berapa node yang dibutuhkan untuk membangun cluster Elasticsearch.

Berikut adalah Rumus dan Best Practisenya

**Rumus**

```
Total Data (GB) = Raw data (GB) per day * Number of days retained * (Number of replicas + 1)
Total Storage (GB) = Total data (GB) * (1 + 0.15 disk Watermark threshold + 0.1 Margin of error)
Total Data Nodes = ROUNDUP(Total storage (GB) / Memory per data node / Memory:Data ratio)+1
```

**Ratio Memory**
```
Hot → 1:30 
Warm → 1:160
Cold → 1:500
```

**Spec Recommendation**

```
Hot Nodes =	8 cores + 64 GB RAM + As per Data size ( add 30 % markup )
Warm Nodes	= 8 cores + 64 GB RAM + As per Data size ( add 30 % markup )
Coordinating Nodes	= 8 cores + 64 GB RAM. + 40 GB SSD
Master Nodes	= 4 cores + 16 GB RAM + 8 GB SSD
Kibana	= 2 cores + 16 GB RAM + 8 GB SSD
Logstash =	8 cores + 16 GB RAM + 16 GB SSD
```

Setelah tau "guideline" perhitungan diatas mari kita lebih deep lagi dalam perhitungannya.

Asumsi ada ingest data tiap hari sebesar = 100 GB / day, yang dimana akan dipisahkan ke Hot, Warm dan Cold tergantung retention berapa lama data di keepnya.

**Retention Keep Data**

1. Hot Nodes = 1 day
2. Warm Nodes = 7 day
3. Cold Nodes = 30 day

Dengan asumsi juga tidak ada replica alias hanya ada 1 copy data aja.

Berikut adalah perhitungannya

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/y1aab31skzp4h1fjen2m.png)

Dari perhitungan ditable diatas ini maka kita membutuhkan **3 Hot Nodes, 3 Warm Nodes dan 3 Cold Nodes.**

Maka apabila kita ingin membangun 1 set cluster elasticsearch maka seperti ini

![Image](https://res.cloudinary.com/brianrakhmataji-id/image/upload/v1702099402/tbjpufoll3kskzeufnda.png)

Dari table diatas bisa kita lihat bahwa kita membutuhkan license Elasticsearch sebanyak 3 Hot Nodes, 3 Warm Nodes dan 3 Cold Nodes, dan 3 Master Nodes **total 12 Nodes**, sedangkan untuk Kibana, Logstash dan Coord Node tidak dihitung license.

Perlu diketahui hitungan diatas ini hanya baru 1 Data Center, apabila temen-temen ingin membangun 2 Data Center, maka tinggal kalikan aja jumlah nodes dan specs nya

Bagaimana gampang bukaaan cara menghitung capacity plan elasticsearch. :D

Buat temen-temen yang ingin excelnya dapat download disini ya [https://brii.my.id/calcelk](https://brii.my.id/calcelk)

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih