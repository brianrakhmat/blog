---
title: Kenalan dengan OceanBase DB, si Database terdistribusi cocok untuk Microservices!
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- Oceanbase DB
- Oracle DB
- Microservices
layout: single

header:
  image: "uploads/af2b70eda6414c4d8a584800cf183a74.png"
  og_image: "uploads/af2b70eda6414c4d8a584800cf183a74.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: OceanBase DB adalah sebuah Database Terdistribusi Opensource DB besutan Alibaba Group, yang di design untuk support high-concurrency, automatic sharding, dan real-time analytics. Saat ini OceanBase banyak digunakan oleh perusahaan China dan beberapa perusahaan di Indonesia seperti Dana.

---

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019183/public/grs17twl5iwne0xvlnls.png)

## **Overview Oceanbase DB**

OceanBase is a commercial database management system that was developed by Alibaba Group. It is designed to support high-concurrency, high-performance OLTP workloads, and offers features such as distributed transaction processing, automatic sharding, and real-time analytics. OceanBase is widely used in China and is gaining popularity in other parts of the world as well.​

OceanBase Database is an enterprise-grade Distributed Database Management System (DBMS) with excellent transactional and analytical processing capabilities. ​

As a proprietary DBMS, OceanBase Database supports both Hybrid Transactional and Analytical Processing (HTAP) with a single architecture, which combines the high scalability of a distributed system and the high efficiency of a centralized system.​

OceanBase Database provides the same atomicity, consistency, isolation, and durability (ACID) capability in both centralized and distributed modes. ​

OceanBase Database ranks No.1 in the TPC-C (Transaction Processing Performance Council) benchmark test with a performance result of 707.35 million tpmC and ranks No.2 in the TPC-H benchmark test with a performance result of 15.26 million QphH@30,000 GB.​

OceanBase Database has supported the stable and efficient operation of core business systems of customers in various industries, such as banking, insurance, transportation, and telecommunications.​

## **Key Feature Oceanbase**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019291/public/fqfuleou8w7qndtoyt7g.png)

## **Client Oceanbase**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019406/public/bvpnlw2xgsceyf4tyqmy.png)

## **Architecture Oceanbase**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019472/public/fwkcqxlu6wrskxnoyvsl.png)

## **Comparison Oceanbase vs Oracle DB**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019625/public/opdfoeoqj5zqcu9r8i5i.png)

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019712/public/mabmtbvyxe9lriikla4q.png)

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019796/public/s3me45ejzocsdbk7qjja.png)

## **Architecture POC Oceanbase**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702019936/public/onxgl5liukzgptak9ml9.png)

## **Scenario Testing via JMeter and Springboot**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702020026/public/acjpwbadrrkad4ommxa4.png)

## **Pro & Cons**

![Image](http://res.cloudinary.com/dr15yjl8w/image/upload/v1702020174/public/fbopb8iqforyipjitdsy.png)

## **Kesimpulan**

Dalam pengujian POC Oceanbase didapakan hasil yang cukup Oke Ketika 1 node dimatikan ada error namun perlahan akan turun.

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih