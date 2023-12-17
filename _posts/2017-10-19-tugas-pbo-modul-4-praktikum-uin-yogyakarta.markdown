---
title: Tugas PBO Modul 4 Praktikum UIN Yogyakarta
date: 2017-10-19 21:23:00 +07:00
categories:
- Tugas
tags:
- Java
- PBO
excerpt: |-
  1. Buatlah program untuk menentukan total uang yang harus dibayar oleh pembeli dengan ketentuan sebagai berikut:
     • Bila total belanja < 500.000 maka diskon 5%
     • Bila total belanja 500.000-1000.000 maka diskon 10%
     • Bila total belanja >1000.000 maka diskon 15%
image: "/uploads/oop.png"
---

1. Buatlah program untuk menentukan total uang yang harus dibayar oleh pembeli dengan ketentuan sebagai berikut:
   • Bila total belanja < 500.000 maka diskon 5%
   • Bila total belanja 500.000-1000.000 maka diskon 10%
   • Bila total belanja >1000.000 maka diskon 15%

```
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package hitung.belanja;

import java.util.Scanner;

/**
 *
 * @author brianrakhmat
 */
public class HitungBelanja {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
        Scanner input = new Scanner(System.in);
        double diskon,harga,jumlah,total=0;
        double diskon1,diskon2,diskon3;
            System.out.print("Masukan Harga Barang: ");
                harga=input.nextInt();
            System.out.print("Jumlah Barang: ");
                jumlah= input.nextInt();
                total= harga*jumlah;
            System.out.println("Total Bayar = "+total);
                diskon1=(total-(total*0.05));
                diskon2=(total-(total*0.1));
                diskon3=(total-(total*0.15));
        if (total>1000000){
            System.out.println("Diskon 15% : " +diskon3);
        }
        else if((total<=1000000)&&(total>=500000)){
            System.out.println("Diskon 10% : "+diskon2);
        }
        else {
            System.out.println("Diskon 5%: "+diskon1);
        }
    }
    
}
```

2. Buatlah program untuk konversi dari bilangan biner ke desimal!
Contoh sekenario:
String bilBiner = “1010”;
//proses konversi
int bilDesimal = …//untuk menampung hasil konversi
System.out.println(bilDesimal); hasil 10

Biner.java
```
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package biner;

import java.util.Scanner;

/**
 *
 * @author brianrakhmat
 */
public class Biner {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
         Scanner input = new Scanner(System.in);
         String bil;
         int [] arr_bil =new int[1000];
         String [] st = new String[1000];
         double hasil=0,result=0;
         int a=0;
         char t;
         System.out.println("Masukan Bilangan Biner : ");
         bil= input.next();
         for(int i=0;i<bil.length();i++){
             t=bil.charAt(i);
             st[i]=Character.toString(t);
         }
         for (int i=bil.length()-1;i>=0;i--){
             arr_bil[a]=Integer.parseInt(st[i]);
             hasil= arr_bil[a]*(Math.pow(2, a));
             result=result+hasil;
             a++;
         }
         {
             int resultIn = (int)result;
             System.out.println("Bilangan Desimal :"+bil);
             System.out.println("Bilangan Biner :"+resultIn);
         }
    }
    
}
```

MainClass.java
```
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package biner;

import java.util.Scanner;

/**
 *
 * @author brianrakhmat
 */
public class MainClass {
    Scanner scan = new Scanner(System.in);
    int num;
    void KonversiNilai(){
    System.out.println("Konversi Biner ke Decimal");
    System.out.println("Masukan Bilangan Biner : ");
    num = Integer.parseInt(scan.nextLine(),2);
    System.out.println("Hasil Konversi Bilangan Desimal:"+num);
    }
}

```