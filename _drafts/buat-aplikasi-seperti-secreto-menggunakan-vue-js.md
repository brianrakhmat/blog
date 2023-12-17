---
title: Buat Aplikasi Seperti Secreto menggunakan Vue.js
date: 2019-02-15 19:21:16 +07:00
categories:
- programming
header:
  image: "/uploads/1_5pK36MBB4okSPNmnFpmk_Q.png"
  og_image: "/uploads/1_5pK36MBB4okSPNmnFpmk_Q.png"
  caption: 'Photo credit: Istimewa'
excerpt: Pada kesempatan kali ini saya akan berbagi tutorial membuat aplikasi seperti
  Secreto.site yang sempat viral beberapa waktu lalu. Aplikasi ini mengirimkan pesan
  tanpa nama yang dimana aplikasi ini memiliki tagline “The anonymous messaging app.”
---

Pada kesempatan kali ini saya akan berbagi tutorial membuat aplikasi seperti Secreto.site yang sempat viral beberapa waktu lalu. Aplikasi ini mengirimkan pesan tanpa nama yang dimana aplikasi ini memiliki tagline “The anonymous messaging app.” Artikel ini juga pernah tayang di [Medium ](https://medium.com/@brianrakhmat/belajar-buat-aplikasi-vue-js-6b4994bac0db)saya.

## Menyiapkan Project

Pertama sudah install node.js, lalu install package vue-cli

    npm install -g vue-cli

Selanjutnya gunakan vuejs-template webpack yang sudah tersedia [disini](https://github.com/vuejs-templates/webpack)

    vue init webpack <nama-project>

Ikuti perintah pada _command line_ dan gunakan juga vue-router pada saat penginstallan. Jika sudah selesai masuk ke direktori projectmu, lalu install _dependency_ pada _boiler plate_ yang kita gunakan.

    npm install

Jika sudah, coba jalankan aplikasi dengan perintah

    npm run dev

Secara default aplikasi tersebut akan berjalan di port 8080

    localhost:8080

Kamu akan melihat halaman seperti ini pada browser kamu:

![](https://cdn-images-1.medium.com/max/800/1*Ih9vtm2fslzfCGu3l7lHsg.png)Langkah selanjutnya adalah kita akan menginstal beberapa dependecy lain yang akan digunakan dalam project ini.

_install buefy_ (sebagai templatenya)

    npm install buefy --save

_install firebase_ (Untuk menggunakan firebase storage)

    npm install firebase --save

_install vue-google-signin-button_ (Untuk login menggunakan Akun Google)

    npm install vue-google-signin-button --save

_install vue-clipboards_ (Untuk mengcopy alamat URL)

    npm install vue-clipboards --save

_install vue-social-sharing_ (Untuk share link profil)

    npm install vue-social-sharing --save

Jika semua dependencys sudah terinstall semua, langkah selanjutnya adalah mulai coding.

Mengedit **index.html**

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width,initial-scale=1.0">
        <title>Katakan Saja - Platform untuk mengatakan sejujurnya</title>
        <meta name="description" content="Platform untuk mengatakan sejujurnya">
        <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.10/css/all.css" integrity="sha384-+d0P83n9kaQMCwj8F4RJB66tzIwOKmrdb46+porD/OvrJ+37WqIM7UoBtwHO6Nlg"
        crossorigin="anonymous">
        <script type="text/javascript" src="https://apis.google.com/js/api:client.js"></script>
        <meta property="og:image" content="https://image.prntscr.com/image/_rior17fSsyzhx9sftb-DA.png">
      </head>
      <body>
        <div id="app"></div>
        <!-- built files will be auto injected -->
      </body>
    </html>

Didalam source code tesebut ada script client.js google yang digunakan untuk sigin with google dan font awesome sebagai iconnya.

Langkah selanjutnya buka **main.js** pada direktori **/src/main.js** dan edit sebagai berikut:

    // The Vue build version to load with the `import` command
    // (runtime-only or standalone) has been set in webpack.base.conf with an alias.
    import Vue from 'vue'
    import App from './App'
    import router from './router'
    import buefy from 'buefy'
    import 'buefy/lib/buefy.css'
    import GSignInButton from 'vue-google-signin-button'
    import VueClipboards from 'vue-clipboards'
    import SocialSharing from 'vue-social-sharing'
    
    Vue.config.productionTip = false
    Vue.use(buefy, {
      defaultIconPack: 'fas'
    })
    Vue.use(GSignInButton)
    Vue.use(VueClipboards)
    Vue.use(SocialSharing)
    
    /* eslint-disable no-new */
    new Vue({
      el: '#app',
      router,
      components: { App },
      template: '<App/>'
    })

Pada buefy (line 13–15) gunakan default icon pack fonts awesome. File main js ini nantinya akan menginit vue js dengan config yang sudah dibuat tersebut dan me-return template “<App/>”.

Langkah Selanjutnya adalah edit **App.vue** pada **/src/App.vue**

    <template>
      <div id="app">
         <nav id="navbar" ref="navbar" class="navbar is-fixed-top has-shadow is-warning" role="navigation" aria-label="main navigation">
            <div class="navbar-brand">
              <a class="navbar-item" href="/">
                <button class="button is-warning"><i class="fas fa-leaf"></i></button><p style="color: white">Katakan Saja</p>
              </a>
              <button class="button navbar-burger is-warning is-no-outline" data-target="navMenu" @click="spanNavigation()">
                <span></span>
                <span></span>
                <span></span>
              </button>
            </div>
            <div class="navbar-menu is-warning" :class="navbarSpan?'is-active':''" id="navMenu">
              <div class="navbar-end">
                <router-link class="navbar-item" tag="a" :to="'/daftar'"><p style="color: white">Daftar</p></router-link>
              </div>
            </div>
        </nav>
        <router-view/>
        <div class="navbar is-fixed-bottom is-light" style="align-item:center">
          <div class="is-footer-content"><router-link tag="a" :to="'/contact'"><p>Kontak</p></router-link></div>
        </div>
      </div>
    </template>
    
    <script>
    export default {
      name: 'App',
      data () {
        return {
          navbarSpan: false
        }
      },
      methods: {
        spanNavigation () {
          this.navbarSpan = !this.navbarSpan
        }
      }
    }
    </script>
    
    <style>
    @import url('https://fonts.googleapis.com/css?family=Roboto:300');
    #app {
      font-family: 'Roboto', sans-serif;
      margin-top: 60px;
    }
    .is-footer-content{
      font-size: 10pt;
      display: flex;
      align-items:center;
      width: 100%;
      justify-content: center;
    }
    </style>
    

pada komponen **App.vue** ini kita akan membuat layout aplikasi, yatu navbar, content-loader dan footer

![](https://cdn-images-1.medium.com/max/800/1*3YEYTE_Qq3ctR0Y2w0J_FQ.png)

Dari layout aplikasi yang terdiri dari navbar, vue-router dan footer.

Aplikasi ini terdiri dari 4 components: **Home**, **Register**, **User**, **Contact**.

Langkah selanjutnya buat component **Home.vue** di direktori **/src/components**

    <template>
      <div style="padding-bottom:60px">
        <section class="section">
          <div class="container">
            <div class="has-text-centered">
              <button class="button is-warning" style="margin-bottom:30px"><i class="fas fa-leaf unguiconcolor"></i></button>
              <h1 class="title">Katakan Saja</h1>
              <h3> Platform Katakan Saja <b><i>Kepada Temanmu</i></b></h3>
              <br>
              <div class="columns">
                <div class="column is-3"></div>
                <div class="column is-6">
                  <div class="box">
                    <h2 class="title">
                    Katakan Saja Kepada Temanmu seperti Secreto
                  </h2>
                  <hr>
                  <router-link class="button is-info" tag="a" :to="'/daftar'">Daftar</router-link>
                  </div>
                </div>
                <div class="column is-3"></div>
              </div>
            </div>
          </div>
        </section>
      </div>
    </template>
    
    <script>
    import * as firebase from 'firebase'
    import 'firebase/firestore'
    const config = {
      apiKey: '', //masukan apikey
      authDomain: '', //masukan auth domain
      databaseURL: '', //masukan db url
      projectId: '', //masukan id project
      storageBucket: '', //masukan bucket storage
      messagingSenderId: '' //masukan sender ID
    }
    firebase.initializeApp(config)
    const db = firebase.firestore()
    export default {
      name: 'Home',
      data () {
        return {
          Messages: [],
          kata2mu: null,
          loading: true
        }
      },
      methods: {
        getAllMessageFromFirebase () {
          const vueContext = this
          const messageRef = db.collection('katakan-saja') //nama db pada firestore
          messageRef.orderBy('timestamp', 'desc').get().then(function (querySnapshot) {
            let messageData = []
            querySnapshot.forEach(function (doc) {
              messageData.push(doc.data())
            })
            vueContext.Messages = messageData
            vueContext.loading = false
          })
        },
        addKatakanToFirebase () {
          const vueContext = this
          const messageRef = db.collection('katakan-saja') //nama db pada firestore
          const timeStamp = firebase.firestore.FieldValue.serverTimestamp()
          vueContext.loading = true
          messageRef.add({
            message: vueContext.kata2mu,
            timestamp: timeStamp
          })
            .then(function (docRef) {
              vueContext.getAllMessageFromFirebase()
            })
            .catch(function (error) {
              console.error('Error : ', error)
              vueContext.loading = false
              vueContext.$snackbar.open({
                duration: 5000,
                message: 'Kata-Katamu gagal dikirim!',
                type: 'is-danger',
                position: 'is-bottom-left',
                actionText: 'Kembalikan',
                queue: false,
                onAction: () => {
                  vueContext.addKatakanToFirebase()
                }
              })
            })
        }
      },
      mounted () {
        this.getAllMessageFromFirebase()
      }
    }
    </script>
    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style scoped>
      .is-no-outline{
        border-radius: 0px;
        border:0px;
      }
      .is-footer-content{
        font-size: 10pt;
        display: flex;
        align-items:center;
        width: 100%;
        justify-content: center;
      }
      .katakan{
        font-size:11pt;
        font-style: italic;
      }
      .is-roundedfull{
        width: 40px;
        height: 40px;
        border-radius:50%;
      }
      .box2{
        border: 1px solid rgb(247, 245, 245);
        background:#f5f5f5;
        padding: 20px 20px 20px 20px;
        border-radius:5px 5px 5px 5px;
      }
      .messages{
        margin-top: 20px;
        margin-bottom: 20px;
      }
      .unguiconcolor {color:#ffffff;}
    </style>

buat component **Register.vue** di direktori **/src/components**

    <template>
      <div>
        <section class="section">
          <div class="container">
            <div class="columns">
              <div class="column"></div>
              <div class="column has-text-centered">
                <div class="box">
                  <i class="fas fa-user-circle fa-5x" v-if="!isRegistered"></i>
                  <div v-if="isRegistered">
                    <img :src="profile.Paa" :alt="profile.U3" class="is-have-border">
                    <h1>{{profile.ig}}</h1>
                  </div>
                  <hr>
                  <h1>{{message}}</h1>
                </div>
                <div v-if="isRegistered">
                  <input type="text" class="input is-small" v-model="url">
                  <br><br>
                  <router-link class="button is-info" tag="a" :to="'/user/'+ profile.Eea">Lihat Halaman Saya</router-link>
                  <button class="button is-info" v-clipboard="url" @click="toastCopy">
                    <i class="fas fa-copy"> Salin URL</i>
                  </button>
                </div>
                <br>
                <g-signin-button
                  :params="googleSignInParams"
                  @success="onSignInSuccess"
                  @error="onSignInError">
                  <i class="fab fa-google"> {{btnGoogle}}</i>
                </g-signin-button>
                <br><br>
                Bagikan :
                <social-sharing :url="url" title="Katakan Saja - Platform untuk mengatakan sejujurnya"
                          description="Platform untuk mengatakan sejujurnya." inline-template>
                    <div>
                        <network network="facebook">
                            <button class="button is-info">
                                <i class="fab fa-facebook"></i>
                            </button>
                        </network>
                        <network network="twitter">
                            <button class="button is-info">
                                <i class="fab fa-twitter"></i>
                            </button>
                        </network>
                        <network network="whatsapp">
                            <button class="button is-info">
                                <i class="fab fa-whatsapp"></i>
                            </button>
                        </network>
                    </div>
                </social-sharing><br>
              </div>
              <div class="column"></div>
            </div>
          </div>
        </section>
      </div>
    </template>
    <script>
    import * as firebase from 'firebase'
    import 'firebase/firestore'
    const db = firebase.firestore()
    export default {
      name: 'register',
      data () {
        return {
          /**
           * The Auth2 parameters, as seen on
           * https://developers.google.com/identity/sign-in/web/reference#gapiauth2initparams.
           * As the very least, a valid client_id must present.
           * @type {Object}
           */
          googleSignInParams: {
            client_id: '' //Dapatkan IDnya dari https://developers.google.com/identity/sign-in/web/sign-in
          },
          profile: null,
          isRegistered: false,
          message: 'Daftar untuk menampung kata-kata dari teman-teman mu!',
          url: null,
          btnGoogle: 'Daftar dengan Google'
        }
      },
      methods: {
        onSignInSuccess (googleUser) {
          const vueInstance = this
          const messageRef = db.collection('user') //nama db untuk menyimpan user
          const rawProfile = googleUser.getBasicProfile() // etc etc
          const uId = googleUser.getId()
          messageRef.doc(uId).set({
            pictures: rawProfile.Paa,
            email: rawProfile.U3,
            name: rawProfile.ig
          })
            .then(function (docRef) {
              vueInstance.profile = rawProfile
              vueInstance.isRegistered = true
              vueInstance.message = 'Halaman Katakan Saja telah dibuat, Bagikan ke teman anda Sekarang!'
              vueInstance.url = 'https://katakan.azurewebsites.net/user/' + uId
              localStorage.setItem('profile', JSON.stringify(rawProfile))
            })
            .catch(function (error) {
              vueInstance.$snackbar.open(error)
            })
        },
        onSignInError (error) {
          this.$snackbar.open(error)
        },
        toastCopy () {
          this.$toast.open({
            position: 'is-bottom',
            message: `copied`
          })
        }
      },
      mounted () {
        const vueInstance = this
        if (localStorage.getItem('profile')) {
          const data = JSON.parse(localStorage.getItem('profile'))
          vueInstance.profile = data
          vueInstance.isRegistered = true
          vueInstance.message = 'Halaman Katakan Saja telah dibuat, Bagikan ke teman anda Sekarang!'
          vueInstance.url = 'https://katakan.azurewebsites.net/user/' + data.Eea
          vueInstance.btnGoogle = 'Pake Akun Lain'
        }
      }
    }
    </script>
    <style scoped>
      .g-signin-button {
        /* This is where you control how the button looks. Be creative! */
        display: inline-block;
        padding: 4px 8px;
        border-radius: 3px;
        background-color: #3c82f7;
        color: #fff;
        box-shadow: 0 3px 0 #0f69ff;
        cursor:pointer;
      }
      .is-have-border{
         border-radius: 50%;
         box-shadow: 2px 1px 0 #0000005b;
      }
    </style>

buat component **User.vue** di direktori **/src/components**

    <template>
      <div style="padding-bottom:60px">
        <section class="section">
          <div class="container">
            <div class="has-text-centered">
              <div class="columns">
                <div class="column is-3"></div>
                <div class="column is-6">
                  <div v-if="profile">
                    <img :src="profile.pictures" :alt="profile.U3" class="is-have-border">
                    <h1>KIRIM KATA-KATA SECARA RAHASIA KEPADA</h1>
                    <h1><b>{{profile.name}}</b></h1>
                    <br>
                  </div>
                  <li>Tenang, {{profile.name}} ga bakal tahu siapa yang ngirim kata-kata</li>
                  <textarea class="textarea" placeholder="Tulis Kata-Kata Rahasiamu!" v-model="kata2mu"></textarea>
                  <br>
                  <button class="button is-info is-small" @click="addKatakanToFirebase">Katakan Pada {{profile.name}}</button>
                  <!-- content here -->
                  <div style="margin-top:30px">
                    <div class="has-text-centered" :class="!loading?'is-hidden':''">
                      <i class="fas fa-spinner fa-spin"></i>
                    </div>
                    <div v-for="(key, index) in Messages" :key="index" class="messages">
                      <article class="media">
                        <div class="media-left">
                            <button class="button is-roundedfull is-warning"> <i class="fas fa-envelope"></i></button>
                        </div>
                        <div class="box2 media-content">
                          <div class="content katakan">
                            {{key.message}}
                            <br>
                            <div style="color:gray; font-size:7pt !important" class="has-text-right">{{key.timestamp}}</div>
                          </div>
                        </div>
                      </article>
                    </div>
                    <div class="has-text-centered katakan" v-if="Messages.length === 0" :class="loading?'is-hidden':''">
                      Belum ada data <i class="fa fa-frown"></i>
                    </div>
                  </div>
                </div>
                <div class="column is-3"></div>
              </div>
            </div>
          </div>
        </section>
      </div>
    </template>
    
    <script>
    import * as firebase from 'firebase'
    import 'firebase/firestore'
    const db = firebase.firestore()
    export default {
      name: 'Home',
      data () {
        return {
          Messages: [],
          kata2mu: null,
          loading: true,
          profile: null
        }
      },
      methods: {
        getAllMessageFromFirebase () {
          const vueContext = this
          const uId = vueContext.$route.params.uId
          const messageRef = db.collection(uId)
          messageRef.orderBy('timestamp', 'desc').get().then(function (querySnapshot) {
            let messageData = []
            querySnapshot.forEach(function (doc) {
              messageData.push(doc.data())
            })
            vueContext.Messages = messageData
            vueContext.loading = false
          })
            .catch(function (error) {
              vueContext.loading = false
              vueContext.$snackbar.open(error)
            })
        },
        getProfile () {
          const vueContext = this
          const uId = vueContext.$route.params.uId
          const messageRef = db.collection('user')
          messageRef.doc(uId).get()
            .then(function (doc) {
              if (doc.exists) {
                vueContext.profile = doc.data()
              } else {
                console.log('No such document!')
              }
            })
            .catch(function (error) {
              vueContext.$snackbar.open(error)
            })
        },
        addKatakanToFirebase () {
          const vueContext = this
          const uId = vueContext.$route.params.uId
          const messageRef = db.collection(uId)
          const timeStamp = firebase.firestore.FieldValue.serverTimestamp()
          vueContext.loading = true
          messageRef.add({
            message: vueContext.kata2mu,
            timestamp: timeStamp
          })
            .then(function (docRef) {
              vueContext.getAllMessageFromFirebase()
            })
            .catch(function (error) {
              console.error('Error : ', error)
              vueContext.loading = false
              vueContext.$snackbar.open({
                duration: 5000,
                message: 'Kata-Katamu gagal dikirim!',
                type: 'is-danger',
                position: 'is-bottom-left',
                actionText: 'Kembalikan',
                queue: false,
                onAction: () => {
                  vueContext.addKatakanToFirebase()
                }
              })
            })
        }
      },
      mounted () {
        this.getAllMessageFromFirebase()
        this.getProfile()
      }
    }
    </script>
    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style scoped>
      .is-no-outline{
        border-radius: 0px;
        border:0px;
      }
      .is-footer-content{
        font-size: 10pt;
        display: flex;
        align-items:center;
        width: 100%;
        justify-content: center;
      }
      .katakan{
        font-size:11pt;
        font-style: italic;
      }
      .is-roundedfull{
        width: 40px;
        height: 40px;
        border-radius:50%;
      }
      .box2{
        border: 1px solid rgb(247, 245, 245);
        background:rgb(252, 252, 252);
        padding: 20px 20px 5px 20px;
        border-radius:0px 10px 10px 15px;
      }
      .messages{
        margin-top: 20px;
        margin-bottom: 20px;
      }
      .is-have-border{
         border-radius: 50%;
         box-shadow: 2px 1px 0 #0000005b;
      }
    </style>

buat component **Contact.vue** di direktori **/src/components**

    <template>
      <div style="padding-bottom:60px">
        <section class="section">
          <div class="container">
            <div class="has-text-centered">
              <div class="columns">
                <div class="column is-3"></div>
                <div class="column is-6">
                    <div class="box">
                        <h1>Contact:</h1><br>
                        <p>Aplikasi ini hanya untuk iseng belaka <br>
                            Dibuat menggunakan Vue.JS, Buefy, dan Firestore <br>
                            brianetlab@gmail.com<br>
                            https://brianrakhmat.github.io
                        </p>
                    </div>
                </div>
                <div class="column is-3"></div>
              </div>
            </div>
          </div>
        </section>
      </div>
    </template>
    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style scoped>
      .is-no-outline{
        border-radius: 0px;
        border:0px;
      }
      .is-footer-content{
        font-size: 10pt;
        display: flex;
        align-items:center;
        width: 100%;
        justify-content: center;
      }
      .pisuhan{
        font-size:11pt;
        font-style: italic;
      }
      .is-roundedfull{
        width: 40px;
        height: 40px;
        border-radius:50%;
      }
      .box2{
        border: 1px solid rgb(247, 245, 245);
        background:rgb(252, 252, 252);
        padding: 20px 20px 5px 20px;
        border-radius:0px 10px 10px 15px;
      }
      .messages{
        margin-top: 20px;
        margin-bottom: 20px;
      }
      .is-have-border{
         border-radius: 50%;
         box-shadow: 2px 1px 0 #0000005b;
      }
    </style>

Setelah 4 Components tadi dibuat langkah selanjutnya adalah mengatur routingnya edit file **index.js** pada **/src/router/index.js** , file tersebut berisi rout aplikasi. Konten yang kamu buat akan dirender pada komponen **App.vue** bagian vue-router.

    import Vue from 'vue'
    import Router from 'vue-router'
    import Home from '@/components/Home'
    import Register from '@/components/Register'
    import User from '@/components/User'
    import Contact from '@/components/Contact'
    
    Vue.use(Router)
    
    export default new Router({
      mode: 'history',
      routes: [
        {
          path: '/',
          name: 'Home',
          component: Home
        },
        {
          path: '/daftar',
          name: 'Register',
          component: Register
        },
        {
          path: '/user/:uId',
          name: 'User',
          component: User
        },
        {
          path: '/contact',
          name: 'Contact',
          component: Contact
        }
      ]
    })

Sampai disini kamu sudah bisa menjalankan aplikasi tersebut dengan menjalankan perintah

    npm run dev

dan ketikan [**http://localhost:8080**](http://localhost:8080/) pada browser

![](https://cdn-images-1.medium.com/max/800/1*5pK36MBB4okSPNmnFpmk_Q.png)

Langkah selanjutnya saya akan menjelaskan cara mendeploy aplikasi ini ke dalam azure websites pada tutorial lainnya.

Demo aplikasi: [**https://katakan.azurewebsites.net**](https://katakan.azurewebsites.net "https://katakan.azurewebsites.net")

Thanks for tutorial [vuejs](http://medium.com/@iqbaladinur) mas Iqbal