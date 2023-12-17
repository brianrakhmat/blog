---
title: Deteksi Ketinggian Banjir berbasis NodeMCU dan Blynk
date: 2017-10-21 19:08:00 +07:00
categories:
- programming
tags:
- IoT
- Arduino
excerpt: 'Alat Deteksi Ketinggian Banjir ini terhubung dengan aplikasi blynk akan
  memonitoring setiap ketinggian air. Setiap data ketinggian airnya akan selalu diupdate
  di aplikasi Blynk. Dari aplikasi ini juga bisa mengirimkan notifikasi setiap status
  airnya dalam keadaan aman,waspada, atau berbahaya. Ketika ketinggian air berada
  dalam batas minimum maka akan menunjukan lampu indikator berwarna hijau. '
image: "/uploads/Deteksi%20Banjir.jpg"
---

## ABOUT THIS PROJECT
Alat deteksi ketinggian banjir ini berfungsi memonitoring ketinggian air sebagai antisipasi bahaya banjir.

## THINGS USED IN THIS PROJECT

**Hardware components:**
* NodeMCU ESP8266 Breakout Board
* Buzzer
* Water Level Sensor
* Breadboard
* LED
* USB-A to Micro USB Cale

**Software apps and online services:**
* Arduino IDE
* Blynk

## STORY
{% include video id="CNfj7LIul-8" provider="youtube" %}

Alat Deteksi Ketinggian Banjir ini terhubung dengan aplikasi blynk akan memonitoring setiap ketinggian air. Setiap data ketinggian airnya akan selalu diupdate di aplikasi Blynk. Dari aplikasi ini juga bisa mengirimkan notifikasi setiap status airnya dalam keadaan aman,waspada, atau berbahaya. Ketika ketinggian air berada dalam batas minimum maka akan menunjukan lampu indikator berwarna hijau. Jika ketinggian air berada di atas batas minimum maka akan menunjukan lampu indikator berwarna kuning. Dan jika ketinggian air berada dibawah batas maksimum maka akan menunjukan lampu indikator berwarna merah dan buzzer akan berbunyi sebagai alarm.

Alat ini diharapkan dapat membantu masyarakat yang ada di hilir sungai sehingga dapat mempersiapkan diri datangnya banjir. Alat ini juga dilengkapi dengan aplikasi android sehingga mempermudah user melihat ketinggian airnya.

**Petunjuk Pembuatan Alat:**
1. Siapkan rangkaian seperti dibawah ini
![Image](https://hackster.imgix.net/uploads/attachments/337307/g4431_oOuE3Ki6Yd.png?auto=compress%2Cformat&w=680&h=510&fit=max)
a. LED Hijau :

- (Kutub +) sambungkan dengan pin Digital D1

- (Kutub -) sambungkan dengan G

b. LED Kuning :

- (Kutub +) sambungkan dengan pin Digital D2

- (Kutub -) sambungkan dengan G

c. LED Merah :

- (Kutub +) sambungkan dengan pin Digital D3

- (Kutub -) sambungkan dengan G

d. Buzzer:

- (Kutub +) sambungkan dengan pin Digital D4

- (Kutub -) sambungkan dengan G

e. Water Level Sensor :

- (Kutub +) sambungkan dengan tegangan 3.3v

- (Kutub -) sambungkan dengan G

- (Kutub S) sambungkan dengan Sinyal Analog A0

2. Download library Blynk :

https://github.com/blynkkk/blynk-library/releases/tag/v0.4.8

3. Masukan library Blynk ke Arduino IDE.

4. Sambungkan Node Mcu ke laptop untuk mengupload program. Pastikan port nya terbaca.

5. Upload code program Deteksi ketinggian banjir sampai proses upload berhasil.

**Cara menyeting aplikasi Blynk untuk membaca data dan membuat notifikasi:**
![Image](https://hackster.imgix.net/uploads/attachments/337309/g4243_GV1gmf0JE2.png?auto=compress%2Cformat&w=680&h=510&fit=max)

1. Buka aplikasi Blynk > pilih New Project.

2. Isi kolom nama project, pilih device Node MCU, pilih tipe koneksi WIFI.

3. Setelah itu maka token akan dikirim ke email.

4. Pilih beberapa witget yang dibutuhkan seperti Notification,Email,Eventor, dan Graph

5. Klik widget Graph lalu setting inputnya menjadi V1 dengan rentang 0-600.

6. Untuk menyeting notifikasi klik widget Eventor lalu isi Eventnya.

7. Jalankan aplikasi dengan menekan icon segitiga di pojok kiri atas.

## SCHEMATICS

** Rancangan Desain Hardware**
![Image](https://halckemy.s3.amazonaws.com/uploads/attachments/336648/orkom_3_j1xvPnEIua.png)

## CODE

** Code Deteksi Ketinggian Banjir C/C++
```
#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

// Authorization token from the Blynk App.
char auth[] = "7683eab38c524f71869e07cd3affda1f";

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "ALHUSNA";
char pass[] = "wetgareng";


const int sensorPin= A0;
float liquid_level;
int liquid_graph;
const int LedHijau = D1;
const int LedKuning = D2;
const int LedMerah = D3;
const int Buzzer = D4;
const int BatasBawah = 250;
const int BatasAtas = 550;

        void setup() {
          Serial.begin(9600);
          Blynk.begin(auth, ssid, pass);
          pinMode(LedMerah, OUTPUT);
          pinMode(LedHijau, OUTPUT) ;
          pinMode(LedKuning, OUTPUT) ;
          pinMode (Buzzer, OUTPUT);
          pinMode(sensorPin, INPUT);
          Blynk.virtualWrite(V0, liquid_level);
          Blynk.virtualWrite(V1, liquid_graph);//This wil show the percentage of water in the container in a virtual pin V1
          Blynk.run();
        // initialize the LED pin as an output:
        pinMode(LedMerah, OUTPUT);
        pinMode(LedHijau, OUTPUT) ;
        pinMode(LedKuning, OUTPUT) ;
        pinMode (Buzzer, OUTPUT);
        // initialize serial communications:
        
        }

        void loop() {
        // read the value of the potentiometer:
        liquid_level = analogRead(sensorPin);
        liquid_graph =analogRead(sensorPin);//Percentage of water in the container 
        Serial.println(liquid_level);//This will print the liquid level in the monitor 
        Serial.println(liquid_graph);//This will print the percentage of liquid in the monitor
        Blynk.virtualWrite(V0, liquid_level);
        Blynk.virtualWrite(V1, liquid_graph);
        
        Blynk.run();
        int analogValue = analogRead(sensorPin);

        // if the analog value is high enough, turn on the LED:
        if (analogValue < BatasBawah) {
         digitalWrite(LedHijau, HIGH);
        } else {
         digitalWrite(LedHijau, LOW);
        }

        if (analogValue > BatasBawah ) {
        digitalWrite(LedKuning, HIGH);
        } else {
        digitalWrite(LedKuning, LOW);
        }

       if (analogValue > BatasAtas) {
       digitalWrite(LedKuning, LOW);
       digitalWrite(LedMerah, HIGH);
       digitalWrite(Buzzer , HIGH);
       
   
      } else {
       digitalWrite(LedMerah, LOW);
       digitalWrite(Buzzer , LOW);

      }
      // print the analog value:
      Serial.println(analogValue);
      delay(100);        // delay in between reads for stability
    }
```

Refrensi: [Erna Novia Safitri](https://dirakit.hackster.io/ernanoviasafitri/deteksi-ketinggian-banjir-berbasis-nodemcu-dan-blynk-3d25db?ref=channel&ref_id=43423_updated___&offset=25)