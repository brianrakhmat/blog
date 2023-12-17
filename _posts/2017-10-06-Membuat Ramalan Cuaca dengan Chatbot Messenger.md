---
title: Membuat Ramalan Cuaca dengan Chatbot Messenger
date: 2017-10-06 20:00:00 +0000
categories:
- programming
tags:
- Chatbot
- Facebook
- Messenger
- Cuaca
layout: single
excerpt: Kali ini kita akan membuat Chatbot Messenger untuk mengetahu Ramalan Cuaca
  dengan menggunakan Openweather
image: assets/images/posts/messenger.jpg

---
## PERSIAPAN

Tools yang diperlukan
* Node JS
* Ngrok (Download [https://ngrok.com/download](Disini) )
* Editor Code (VS Code/Sublime/Notepad/dll)

## MULAI

**Buat First Project**

```
npm init
```

Disini entry pointnya saya buat **app.js** . Lalu kita tambahkan beberapa Framework dan Lib pada Bot kita.

```
npm install express body-parser --save
```

Install:
* Exspress
* Body Parser

Selanjutnya Install Module untuk menjalankan Request

```
npm install request --save
```

**Setup **API.ai****

Api.ai ini untuk menjawab pertanyaan biar gak kaku, untuk sementara bahasa indonesia belum support :(

Buka halaman **https://console.api.ai** lalu register dan buat agent baru, isi yang agentnya saja, biarkan lainnya default.

![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_2.png?alt=media&token=5c36b9a4-d0ab-4445-b7cf-ba17c35291ed)

Setelah itu aktifkan **Smart Talk** untuk kasus ~~salah beli ~~ agar bot kita tidak kaku.

![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%204.09.01%20PM.png)

setelah itu, install module API AI untuk NodeJs

```
npm install apiai
```

**Setting Intent AI**

**buka dan buatlah intent didashboard api.ai**

![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_4.png?alt=media&token=80eb0d5b-a694-4b8d-8975-9d1fec99ab9a)
![Image](https://firebasestorage.googleapis.com/v0/b/img-storage-d41a0.appspot.com/o/images%2FScreenshot_5.png?alt=media&token=40f9e592-218f-492f-ae68-a4ede016668a)

**Create Akun di OpenWeatherMap**

Buat akun dan setelah itu salin **API Key** nya

## Setting Facebook Developer

**Create Facebook Page**
```
http://facebook.com/pages/create
```

![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%2012.49.28%20PM.png)

Pilih bebas halamannya:

![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%2012.53.17%20PM.png)

langkah selanjutnya adalah membuat aplikasi di Facebook

## Membuat App di Facebook
```
https://developers.facebook.com/quickstarts/?platform=web
```

![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%2012.59.40%20PM.png)

menuju dashboard Facebook Apps
![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%201.00.22%20PM.png)

Tambahkan Produk **Messenger**

![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%201.01.23%20PM.png)

setelah disiapkan, geser kebawah untuk membuat Token
![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%201.03.28%20PM.png)

kemudian setting untuk webhook yang sudah dibuat diawal
![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%201.06.55%20PM.png)

klik Verifikasi dan Simpan, jika URL Callback sudah OK maka hasilnya nanti adalah Tersimpan
![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%201.08.57%20PM.png)

**Coding **App.js***
```
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
const request = require('request');
const API_TOKEN = "39e70b551e0140d5bd9debf1b022e2b0"; //Token FB
const aiApp    = require('apiai')(API_TOKEN);
const VALID_TOKEN   = "ACVBnm"; //Bebas mau apa aja
const SERVER_URL    = "https://c43f8216.ngrok.io"; //Setelah dijalankan ngrok.exe
const ACCESS_TOKEN  = "EAAFoboTScRwBAN2EhAIpUTV87DJG9nov1bkxj37SSmG7LR9sdsIW1ulSR4pOXkJUxU7GEuItuq9Ixqzhyj37EFXBhymXH7DdjiyYQugivZC2LV3V6y7X5jwXZBa2MvEQCY1mTvICoZBddj21UK1klWHwPjCYVgkPTRkRIUHEZAwcgPq1ZAI4h"; //Dari FB Pages
const server = app.listen(process.env.PORT || 5000, () => {
  console.log('Express server listening on port %d in %s mode', server.address().port, app.settings.env);
})

/* Hello Data */
app.get('/', (req, res) => {
    console.log('Server Ok!');
    res.sendStatus(200);
});

app.get('/webhook', (req, res) => {
    if (req.query['hub.mode'] && req.query['hub.verify_token'] === VALID_TOKEN) {
        res.status(200).send(req.query['hub.challenge']);
    } else {
        res.status(403).end();
    }
});

/* Handling Pesan */
app.post('/webhook', (req, res) => {
    //console.log(req.body);
    if (req.body.object === 'page') {
      req.body.entry.forEach((entry) => {
        entry.messaging.forEach((event) => {
          if (event.message && event.message.text) {
            sendMessage(event);
            console.log(event);
          }
        });
      });
      res.status(200).end();
    }
  });

/*function sendMessage(event) {
    let sender = event.sender.id;
    let text = event.message.text;

    
    console.log("Dikirim ke %s ", sender);

    request({
      url: 'https://graph.facebook.com/v2.6/me/messages',
      qs: {access_token: ACCESS_TOKEN},
      method: 'POST',
      json: {
        recipient: {id: sender},
        message: {text: text}
      }
    }, function (error, response) {
      if (error) {
          console.log('Error sending message: ', error);
      } else if (response.body.error) {
          console.log('Error: ', response.body.error);
      }
    });
  }*/

  function sendMessage(event) {
    let sender = event.sender.id;
    let text = event.message.text;

    let apiai = aiApp.textRequest(text, {
      sessionId: 'anakjalananbro'
    });

    apiai.on('response', (response) => {
      // Response ke Facebook messenger
      	let aiText = response.result.fulfillment.speech;
		console.log("response ai %s ", aiText);
		request({
		    url: 'https://graph.facebook.com/v2.6/me/messages',
		    qs: {access_token: ACCESS_TOKEN},
		    method: 'POST',
		    json: {
		        recipient: {id: sender},
		        message: {text: aiText}
		    }
		}, (error, response) => {
		    if (error) {
		        console.log('Error sending message: ', error);
		    } else if (response.body.error) {
		        console.log('Error: ', response.body.error);
		    }
		});
    });

    apiai.on('error', (error) => {
      console.log(error);
    });

    apiai.end();
  }

  const WEATHER_API_KEY   = "7f060ac1edaaa0052b8eae2992eff568"; //API Weather
	app.post('/ai', (req, res) => {
    if (req.body.result.action === 'weather') {
        let city = req.body.result.parameters['geo-city'];
        console.log(city);
        let restUrl = 'http://api.openweathermap.org/data/2.5/weather?APPID='+WEATHER_API_KEY+'&q='+city;
        request.get(restUrl, (err, response, body) => {
            if (!err && response.statusCode == 200) {
                let json = JSON.parse(body);
                let msg = json.weather[0].description + ' and the temperature is ' + json.main.temp + ' ℉';
                return res.json({
                  speech: msg,
                  displayText: msg,
                  source: 'weather'});
              } else {
                return res.status(400).json({
                  status: {
                    code: 400,
                    errorType: 'I failed to look up the city name.'}});
              }
        });
    }
  });
```

**SELAMAT**

![Image](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/assets/Screen%20Shot%202017-09-29%20at%205.32.29%20PM.png)

Jika berhasil anda akan melihat tampilan seperti ini
<br>
<br>

Sumber dan lebih jelasnya dapat membuka module ini: 
[https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/mulai-menulis.html](https://rakaadinugroho.gitbooks.io/facebook-chatbot-with-nlp/content/mulai-menulis.html)

Source Code: 
[https://github.com/brianrakhmat/chatbot-messenger](https://github.com/brianrakhmat/chatbot-messenger)