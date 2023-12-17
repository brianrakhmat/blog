---
title: Solusi Storage hosting kecil dengan Firebase Storage
date: 2017-10-06 19:49:39 +07:00
categories:
- programming
tags:
- firebase
layout: single
excerpt: Firebase adalah layanan DbaaS (Database as a Service) yang dimiliki oleh
  Google, banyak yang dapat dilakukan dengan layanan satu ini yakni cukup mudah dikonfigurasi
  atau mudah dibuat oleh developer
image: assets/images/posts/firebase.png
---

## **Pengantar**
Firebase adalah layanan DbaaS (Database as a Service) yang dimiliki oleh Google, banyak yang dapat dilakukan dengan layanan satu ini yakni cukup mudah dikonfigurasi atau mudah dibuat oleh developer pemula yang ingin belajar mengenai Firebase. Salah satunya adalah Firebase Storage yakni layanan Storage yang disediakan oleh Google pada layanan Firebase, sekarang kita akan membuat Upload Images ke Firebase Storage dengan aplikasi Web.

## **Mengapa Firebase Storage?**
Firebase Storage ini dapat digunakan untuk aplikasi atau website kamu jika resource hosting / server kamu kecil, sedangkan yang kamu butuhkan cukup besar, dan ingin cepat diakses, salah satunya kamu bisa memanfaatkan Firebase Storage ini pada layanan kamu, hal ini dapat menekan pengeluaran belanja server yang cukup lumayan besar.
Apa Bedanya Firebase Storage vs Google Drive?
Firebase Storage atau layanan Google Cloud memang di desain untuk kalangan developer/programmer sehingga penggunaannya perlu skill programming, sedangkan Google Drive siapapun bisa menggunakannya secara mudah.

## **Pesiapan**
* Sudah punya akun Google
* Sudah punya layanan Firebase
* Mengerti mengenai HTML/CSS/Javascript

Jika semuanya sudah mari kita buat aplikasi sederhana upload gambar menggunakan Firebase Storage.

## #**Firebase**
* Login Ke Firebase > Go To Console (https://firebase.google.com)
* Buat Proyek

![Image](https://cdn-images-1.medium.com/max/800/1*sxGrL-kKqXfxOqlsYnJLmg.jpeg)

Nama Proyek: img-storage
Negara/Wilayah: Indonesia

* Tambahkan Firebase ke aplikasi web anda

![Image](https://cdn-images-1.medium.com/max/800/1*dRRKIw5EfPCvm6BTSr5TkA.jpeg)

* Salin Script berikut, ini digunakan untuk script upload

![Image](https://cdn-images-1.medium.com/max/800/1*2keHNH9nsOXr22Zm_Hoz_w.jpeg)

* Klik Storage, lalu buat folder images

![Image](https://cdn-images-1.medium.com/max/800/1*arv0nCGwX32iVBl8TFC00Q.jpeg)

* Atur Rule/Aturan pada Storage (Bucket)

![Image](https://cdn-images-1.medium.com/max/800/1*Z__rF4s0Labk1yPha-5X8w.jpeg)

Ganti *write: if request.auth != null;* menjadi *write: if true;* ini ditujukan agar file dapat diupload disini.

## **#HTML**

```
<!DOCTYPE html>
  <html>
    <head>
      <title>Home</title>
      <!--Import Google Icon Font-->
      <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
      <!--Import materialize.css-->
      <link type="text/css" rel="stylesheet" href="assets/css/materialize.min.css"  media="screen,projection"/>

      <!--Let browser know website is optimized for mobile-->
      <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
      <!--Import jQuery before materialize.js-->
      <script type="text/javascript" src="https://code.jquery.com/jquery-2.1.1.min.js"></script>
      <script type="text/javascript" src="assets/js/materialize.min.js"></script>
      <script src="https://www.gstatic.com/firebasejs/3.4.0/firebase.js"></script>
      <script>
        $(document).ready(function(){
        $(".button-collapse").sideNav();
        $('.materialboxed').materialbox();
        });
      </script>
    </head>
    
    <body>
        <!--Menu & Sidebar start-->
        <nav>
            <div class="container">
                <div class="nav-wrapper">
                    <a href="index.html" class="brand-logo">Home</a>
                    <a href="#" data-activates="mobile-demo" class="button-collapse"><i class="material-icons">menu</i></a>
                        <ul class="right hide-on-med-and-down">
                            <li class="active"><a href="index.html">Home</a></li>
                        </ul>
                        <ul class="side-nav" id="mobile-demo">
                            <li class="active"><a href="index.html">Home</a></li>
                        </ul>
                </div>
            </div>
        </nav>
      <!--Menu & Sidebar end-->

        <div class="container">
            <div class="row">
                <!--Desc-->
                <div class="col s12">
                    <div class="card-panel teal">
                        <span class="white-text"><center>Firebase Storage Upload</center>
                        </span>
                    </div>
                </div>
                <!--Desc-->

                <div class="file-field input-field">
                    <div class="btn">
                        <span>File</span>
                        <input type="file" onchange="previewFile()">
                    </div>
                    <div class="file-path-wrapper">
                        <input class="file-path validate" type="text">
                    </div>
                </div>
                <p id="url"><b>Firebase Storage URL: </b></p>
                <div class="col s12">
                    <img class="responsive-img" src="https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2Ffirebase-storage.jpg?alt=media&token=394aeb7e-c10b-4b02-b7b2-144795ebf4a8" id="preview" alt="Preview Image">
                </div>
            </div>
        </div>
        <footer class="page-footer">   
            <div class="footer-copyright">
                <div class="container">
                © 2017 Brianrakhmat.id
                </div>
            </div>
      </footer>
    </body>
    <script>
        var config = {
        apiKey: "AIzaSyD8saoX0XhzFv24NyqrmGYSJ-lvyEerku8", // Ganti dengan step no 3
        authDomain: "img-storage-d41a0.firebaseapp.com", // Ganti dengan step no 3
        databaseURL: "https://img-storage-d41a0.firebaseio.com", // Ganti dengan step no 3
        projectId: "img-storage-d41a0", // Ganti dengan step no 3
        storageBucket: "img-storage-d41a0.appspot.com", // Ganti dengan step no 3
        messagingSenderId: "337037106958" // Ganti dengan step no 3
        };
        firebase.initializeApp(config);

        var storageRef = firebase.storage().ref();


        var imagesRef = storageRef.child('images');
        function previewFile(){

        var file =document.querySelector('input[type=file]').files[0];

        var metadata = {
        contentType: 'image/jpeg' //Tipe File yang dapat di baca, dapat diganti dengan type lain
        };

        var uploadTask = storageRef.child('images/' + file.name).put(file, metadata); //folder Images pada Storage

        uploadTask.on(firebase.storage.TaskEvent.STATE_CHANGED,
        function(snapshot) {
            var progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
            console.log('Upload is ' + progress + '% done');
            switch (snapshot.state) 
            {
                case firebase.storage.TaskState.PAUSED: 
                    console.log('Upload is paused');
                    break;
                case firebase.storage.TaskState.RUNNING:
                    console.log('Upload is running');
                    break;
            }
        }, 
        function(error) {
            console.log('Upload Error')
        }, 
        function() {
            var starsRef = storageRef.child('images/'+ file.name); //folder Images pada Storage
            starsRef.getDownloadURL().then(function(url) {
                document.querySelector('#preview').src=url;
                var t=document.querySelector('p')
                t.innerHTML ='<b>Firebase Storage URL: </b>'+url
            }).catch(function(error) {
                console.log('Error Download File');
            });
        });
        }
    </script>

</html>
```

Jika berhasil dijalankan akan muncul seperti ini, file akan terupload secara otomatis dan Firebase Storage URL akan tergenerate secara sistematis seperti gambar dibawah ini:

![Image](https://cdn-images-1.medium.com/max/800/1*4nzdsINnl1Ejnx2KMv4vNg.jpeg)

**Demo:** https://img-storage-d41a0.firebaseapp.com/ atau https://demo.brianrakhmataji.com/firebase-storage-tutorial/
**Github:** https://github.com/brianetlab/firebase-storage-tutorial/

## **Kesimpulan**
Firebase Storage ini dapat digunakan pada aplikasi kamu untuk mengunggah file-file yang cukup besar dan ingin cepat diakses karena tidak memerlukan cost yang tinggi untuk membeli atau menyewa server/hostingan. Semoga bermanfaat :)