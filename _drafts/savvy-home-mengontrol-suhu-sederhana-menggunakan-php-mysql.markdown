---
title: Savvy Home - Mengontrol Suhu sederhana Menggunakan PHP MySQL
date: 2017-10-12 10:16:00 +07:00
categories:
- programming
tags:
- Savvy Home
- IoT
- PHP
- MySql
- Mengontrol Suhu
excerpt: Membuat "Rumah Pintar" aplikasi mengontrol suhu sederhana menggunakan PHP
  MySQL
image: "/uploads/img20170809113114_KyiA8xj56d.jpg"
---

## About This Project

Membuat "Rumah Pintar" aplikasi mengontrol suhu sederhana menggunakan PHP MySQL

# Story

Membuat "Rumah Pintar" mengontrol suhu sederhana dengan menggunakan PHP MySQL dengan menggunakan beberapa alat yaitu:

* NodeMCU
* Jumper cables
* Breadboard
* Sensor Suhu LM 35
* LED

![Image](https://hackster.imgix.net/uploads/attachments/337394/img20170809113114_KyiA8xj56d.jpg?auto=compress%2Cformat&w=680&h=510&fit=max)

Hubungkan semua komponen sesuai skema yang ada. Hasil dari skema yang ada akan terbentuk seperti gambar diatas.

ketika sudah disusun seperti skema maka langkah selanjutnya adalah mengupload scrip/code yang telah ada ke nodeMCU, setelah selesai anda dapat melihat hasilnya di video berikut.

{% include youtube_embed.html id="fSA1fnyYLdQ" %}

Untuk skrip PHPnya sudah ada diattachment beserta databasenya (mysql) tinggal langsung import saja. Jalankan aplikasinya via Browser.

## Schematics

![Image](https://halckemy.s3.amazonaws.com/uploads/attachments/336857/esp8266_schematics_bb_O4OceHRLnK.jpg)

## Code

**Sketch**
```
//include libraries
#include <ESP8266HTTPClient.h>
#include <ESP8266WiFi.h> 

//Access point credentials
const char* ssid = "asus zenfone";
const char* pwd = "123456";

int sensor;
float temperature, refvoltage, temp;

int ledPin = 13; //connected to pin 7 in nodemcu 1.0 esp-12e module
WiFiServer server(80);  // open port 80 for server connection

void setup() 
{
  Serial.begin(115200); //initialise the serial communication
  delay(10);

  //defining the pins, i/p and o/p
  pinMode(ledPin, OUTPUT);
  pinMode(A0, INPUT);
  digitalWrite(ledPin, LOW);

   refvoltage = 2.25;   //reference voltage for temperature calculation
        
  //connecting to wifi
  Serial.println();
  Serial.println();
  Serial.print("Connecting to wifi ");
  Serial.println(ssid);

  WiFi.begin(ssid, pwd);
  
  //attempt to connect to wifi
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print("."); //progress with dots until the wifi is connected
  }
    Serial.println("");

    //while connected print this
    Serial.println("Wifi connected");

    //starting the server
    server.begin();
    Serial.println("Server started.");

    //get the ip address and print it
    Serial.print("This is your ip address: ");
    Serial.print("http://");
    Serial.print(WiFi.localIP());
    Serial.println("/");  
}

void loop()
{
     WiFiClient client = server.available();
    if (!client)
    {
      return;
    }
    
    //wait for the data to be sent from client
    Serial.println("New client connection");
    while(!client.available())
    {
      delay(1);
    }

    //Read the first line of the request
    String request = client.readStringUntil('\r');
    Serial.println(request);
    client.flush();
    
   int value = LOW; // set the thermometer off initially
   sensor = analogRead(A0);
   temperature = (refvoltage * sensor * 100) / 1023; //converting degree to celcius
   
    //check the index of the browser and act accordingly 
    if (request.indexOf("/Thermo=ON") != -1) 
    {
        digitalWrite(ledPin, HIGH);
        value = HIGH;
        sensor = analogRead(A0);
        temperature = (refvoltage * sensor * 100) / 1023; //converting degree to celcius
       
        //save the data to mysql, access the php file to write
        HTTPClient http;
        String url = "http://localhost/savvy/add.php?temp="+String(temp);
        Serial.println(url);     
        http.begin(url);
       
        //GET method
        int httpCode = http.GET();
        if(httpCode > 0)
        {
          Serial.printf("[HTTP] GET...code: %d\n", httpCode);
          if(httpCode == HTTP_CODE_OK)
          {
              String payload = http.getString();
              Serial.println(payload);
          }
       }
       else
       {
            Serial.printf("[HTTP] GET... failed, error: %s\n", http.errorToString(httpCode).c_str());
       }
          http.end();
          delay(3000);
   }

    if (request.indexOf("/Thermo=OFF") != -1)
    {
      digitalWrite(ledPin, LOW);
      value = LOW;
    } 
      temp = temperature; 
    
      //Return the response
      client.println("HTTP/1.1 200 OK");
      client.println("Content-Type: text/html");

      if (request.indexOf("/AlwaysOn") != -1) 
      {
        digitalWrite(ledPin, HIGH);
        value = HIGH;
        sensor = analogRead(A0);
        temperature = (refvoltage * sensor * 100) / 1023; //converting degree to celcius
        //temp = temperature; 
        client.println("Refresh: 5");
      }

      client.println("");
      client.println("<!DOCTYPE HTML>");
      client.println("<html>");
      client.println("<body style=background-color:skyblue> </body>");
      client.println("<style> h1 {text-align: center}</style>");
      client.println("<style> h3 {text-align: center}</style>");
      client.println("<style> b {text-align: center}</style>");
      client.println("<style> p {text-align: center}</style>");
      client.println("<head><style>div.relative{position:relative; left:200px; height:20px; width:350px; border:2px solid #73AD21;}</style></head>");
      client.println();

      client.println("<div class=relative>  <b> UIN Suka Yogyakarta  </b> </div>");
      client.println("<div class=relative> Brian Rakhmat Aji  </div>");
      client.println("<div class = relative>  /// </div>");
     
      //client.println("<br>");
      client.println("<br><br><h1>Savvy Home (Monitor Suhu)</h1><br><br>");
      //client.println("<h3>Probable LM35 analog reading: <h3>");
      //client.print(sensor); //analog reading of the sensor
      //client.print("<br>");
      
      client.print("<h3>Thermometer's current status: </h3>");
      if(request.indexOf("/AlwaysOn") != -1)
      {
        client.print("<h3>Always On<h3>");
        client.print("(Temperature updated every 5 seconds.)");
        client.println("<h3>Current Temperature: <h3>");
        client.print(temp);
        client.print("<b> deg C.</b>");

        //save the data to mysql, with http client
      HTTPClient http;
      String url = "http://localhost/savvy/add.php?temp="+String(temp); //access the php file to write data
      Serial.println(url);     
      http.begin(url);

      //using GET method to write to sql
      int httpCode = http.GET();
      if(httpCode > 0)
      {
          Serial.printf("[HTTP] GET...code: %d\n", httpCode);
            if(httpCode == HTTP_CODE_OK)
            {
              String payload = http.getString();
              Serial.println(payload);
            }
      }
         else
         {
            Serial.printf("[HTTP] GET... failed, error: %s\n", http.errorToString(httpCode).c_str());
         }
          http.end();
       //delay(3000);
    }
        
     else if(value == HIGH)
     {
          client.print("<h3>On Once<h3>");
          //client.println("<br>");
          client.println("<h3>Current Temperature: <h3>");
          client.print(temp);
          client.print("<b> deg C.</b>");
          //delay(100);
      }
      else if(value == LOW)
      {
          client.print("<h3>Off<h3>");
         // client.println("<br>"); 
          client.println("<h3>Last measured temperature: <h3>"); //print the last value of temp
          client.print(temp);
          client.print("<b> deg C.</b>");
      }
 
      client.println("<br><br>");
      //create buttons
      client.println("<a href=\"/Thermo=ON\"\"><button>Turn On </button></a>");
      client.println("<a href=\"/AlwaysOn\"\"><button>Keep On </button></a>");
      client.println("<a href=\"/Thermo=OFF\"\"><button>Turn Off </button></a><br />");
      
      client.println("<h3>Check the Temperature records by following the below link: <h3>");
      client.println("<p>http://localhost/savvy/show.php</p>");
      
      // if there are incoming bytes available from the server, read them and print them:
     if (client.available()) 
     {
       char c = client.read();
       client.print(c);
     }
  
      client.println("</html>");
      
      client.println();
      delay(1);
      Serial.println("Client disconnected!");
      Serial.println("");
}
    
   
```

**Suhuhariini.php**
```
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <meta content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" name="viewport">
    <title>Suhu Hari ini</title>
    <!-- Favicon-->
    <link rel="icon" href="../../favicon.ico" type="image/x-icon">

    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css?family=Roboto:400,700&subset=latin,cyrillic-ext" rel="stylesheet" type="text/css">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" type="text/css">

    <!-- Bootstrap Core Css -->
    <link href="../../plugins/bootstrap/css/bootstrap.css" rel="stylesheet">

    <!-- Waves Effect Css -->
    <link href="../../plugins/node-waves/waves.css" rel="stylesheet" />

    <!-- Animation Css -->
    <link href="../../plugins/animate-css/animate.css" rel="stylesheet" />

    <!-- Custom Css -->
    <link href="../../css/style.css" rel="stylesheet">

    <!-- AdminBSB Themes. You can choose a theme from css/themes instead of get all themes -->
    <link href="../../css/themes/all-themes.css" rel="stylesheet" />
</head>

<body class="theme-red">
    <!-- Page Loader -->
    <div class="page-loader-wrapper">
        <div class="loader">
            <div class="preloader">
                <div class="spinner-layer pl-red">
                    <div class="circle-clipper left">
                        <div class="circle"></div>
                    </div>
                    <div class="circle-clipper right">
                        <div class="circle"></div>
                    </div>
                </div>
            </div>
            <p>Please wait...</p>
        </div>
    </div>
    <!-- #END# Page Loader -->
    <!-- Overlay For Sidebars -->
    <div class="overlay"></div>
    <!-- #END# Overlay For Sidebars -->
    <!-- Search Bar -->
    <div class="search-bar">
        <div class="search-icon">
            <i class="material-icons">search</i>
        </div>
        <input type="text" placeholder="START TYPING...">
        <div class="close-search">
            <i class="material-icons">close</i>
        </div>
    </div>
    <!-- #END# Search Bar -->
    <!-- Top Bar -->
    <nav class="navbar">
        <div class="container-fluid">
            <div class="navbar-header">
                <a href="javascript:void(0);" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar-collapse" aria-expanded="false"></a>
                <a href="javascript:void(0);" class="bars"></a>
                <a class="navbar-brand" href="../../index.html">ADMINBSB - MATERIAL DESIGN</a>
            </div>
            <div class="collapse navbar-collapse" id="navbar-collapse">
                <ul class="nav navbar-nav navbar-right">
                    <!-- Call Search -->
                    <li><a href="javascript:void(0);" class="js-search" data-close="true"><i class="material-icons">search</i></a></li>
                    <!-- #END# Call Search -->
                    <!-- Notifications -->
                    <li class="dropdown">
                        <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" role="button">
                            <i class="material-icons">notifications</i>
                            <span class="label-count">7</span>
                        </a>
                        <ul class="dropdown-menu">
                            <li class="header">NOTIFICATIONS</li>
                            <li class="body">
                                <ul class="menu">
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-light-green">
                                                <i class="material-icons">person_add</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4>12 new members joined</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 14 mins ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-cyan">
                                                <i class="material-icons">add_shopping_cart</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4>4 sales made</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 22 mins ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-red">
                                                <i class="material-icons">delete_forever</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>Nancy Doe</b> deleted account</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 3 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-orange">
                                                <i class="material-icons">mode_edit</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>Nancy</b> changed name</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 2 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-blue-grey">
                                                <i class="material-icons">comment</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>John</b> commented your post</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 4 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-light-green">
                                                <i class="material-icons">cached</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>John</b> updated status</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 3 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-purple">
                                                <i class="material-icons">settings</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4>Settings updated</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> Yesterday
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                </ul>
                            </li>
                            <li class="footer">
                                <a href="javascript:void(0);">View All Notifications</a>
                            </li>
                        </ul>
                    </li>
                    <!-- #END# Notifications -->
                    <!-- Tasks -->
                    <li class="dropdown">
                        <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" role="button">
                            <i class="material-icons">flag</i>
                            <span class="label-count">9</span>
                        </a>
                        <ul class="dropdown-menu">
                            <li class="header">TASKS</li>
                            <li class="body">
                                <ul class="menu tasks">
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Footer display issue
                                                <small>32%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-pink" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 32%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Make new buttons
                                                <small>45%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-cyan" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 45%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Create new dashboard
                                                <small>54%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-teal" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 54%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Solve transition issue
                                                <small>65%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-orange" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 65%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Answer GitHub questions
                                                <small>92%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-purple" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 92%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                </ul>
                            </li>
                            <li class="footer">
                                <a href="javascript:void(0);">View All Tasks</a>
                            </li>
                        </ul>
                    </li>
                    <!-- #END# Tasks -->
                    <li class="pull-right"><a href="javascript:void(0);" class="js-right-sidebar" data-close="true"><i class="material-icons">more_vert</i></a></li>
                </ul>
            </div>
        </div>
    </nav>
    <!-- #Top Bar -->
    <section>
        <!-- Left Sidebar -->
        <aside id="leftsidebar" class="sidebar">
            <!-- User Info -->
            <div class="user-info">
                <div class="image">
                    <img src="../../images/user.png" width="48" height="48" alt="User" />
                </div>
                <div class="info-container">
                    <div class="name" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">John Doe</div>
                    <div class="email">john.doe@example.com</div>
                    <div class="btn-group user-helper-dropdown">
                        <i class="material-icons" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">keyboard_arrow_down</i>
                        <ul class="dropdown-menu pull-right">
                            <li><a href="javascript:void(0);"><i class="material-icons">person</i>Profile</a></li>
                            <li role="seperator" class="divider"></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">group</i>Followers</a></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">shopping_cart</i>Sales</a></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">favorite</i>Likes</a></li>
                            <li role="seperator" class="divider"></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">input</i>Sign Out</a></li>
                        </ul>
                    </div>
                </div>
            </div>
            <!-- #User Info -->
            <!-- Menu -->
            <div class="menu">
                <ul class="list">
                    <li class="header">MAIN NAVIGATION</li>
                    <li><a href=""><i class="material-icons">home</i>
                        <span>Home</span></a>
                    </li>
                    <li class="active">
                        <a href="javascript:void(0);" class="menu-toggle">
                            <i class="material-icons">pie_chart</i>
                            <span>Data</span>
                        </a>
                        <ul class="ml-menu">
                            <li class="active">
                                <a href="http://localhost/savvy/pages/charts/chartjs.html">Data Hari Ini</a>
                            </li>
                            <li>
                                <a href="http://localhost/savvy/pages/history.php">History</a>
                            </li>
                        </ul>
                    </li>
                    
                </ul>
            </div>
            <!-- #Menu -->
            <!-- Footer -->
            <div class="legal">
                <div class="copyright">
                    &copy; 2016 <a href="javascript:void(0);">AdminBSB - Material Design</a>.
                </div>
                <div class="version">
                    <b>Version: </b> 1.0.4
                </div>
            </div>
            <!-- #Footer -->
        </aside>
        <!-- #END# Left Sidebar -->
        
    </section>

    <section class="content">
        <div class="container-fluid">
            <div class="block-header">
                <h2>
                    Data hari ini
                   
                </h2>
            </div>
            <div class="row clearfix">
                
                <!-- Bar Chart -->
                <div class="col s12">
                    <div class="card">
                        <div class="header">
                            <h2>Suhu hari ini</h2>
                            <ul class="header-dropdown m-r--5">
                                <li class="dropdown">
                                    <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
                                        <i class="material-icons">more_vert</i>
                                    </a>
                                    <ul class="dropdown-menu pull-right">
                                        <li><a href="javascript:void(0);">Action</a></li>
                                        <li><a href="javascript:void(0);">Another action</a></li>
                                        <li><a href="javascript:void(0);">Something else here</a></li>
                                    </ul>
                                </li>
                            </ul>
                        </div>
                        <div class="body">
                            <canvas id="suhu" height="150"></canvas>
                        </div>
                    </div>
                </div>
                <!-- #END# Bar Chart -->
            </div>

            
    </section>

    <!-- Jquery Core Js -->
    <script src="../../plugins/jquery/jquery.min.js"></script>

    <!-- Bootstrap Core Js -->
    <script src="../../plugins/bootstrap/js/bootstrap.js"></script>

    <!-- Select Plugin Js -->
    <script src="../../plugins/bootstrap-select/js/bootstrap-select.js"></script>

    <!-- Slimscroll Plugin Js -->
    <script src="../../plugins/jquery-slimscroll/jquery.slimscroll.js"></script>

    <!-- Waves Effect Plugin Js -->
    <script src="../../plugins/node-waves/waves.js"></script>

    <!-- Chart Plugins Js -->
    <script src="../../plugins/chartjs/Chart.bundle.js"></script>

    <!-- Custom Js -->
    <script src="../../js/admin.js"></script>
    <script src="../../js/pages/charts/chartjs.js"></script>

    <!-- Demo Js -->
    <script src="../../js/demo.js"></script>
</body>

</html>
```

**History.php**
```
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <meta content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" name="viewport">
    <title>History Suhu</title>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css?family=Roboto:400,700&subset=latin,cyrillic-ext" rel="stylesheet" type="text/css">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" type="text/css">

    <!-- Bootstrap Core Css -->
    <link href="http://localhost/savvy/plugins/bootstrap/css/bootstrap.css" rel="stylesheet">

    <!-- Waves Effect Css -->
    <link href="http://localhost/savvy/plugins/node-waves/waves.css" rel="stylesheet" />

    <!-- Animation Css -->
    <link href="http://localhost/savvy/plugins/animate-css/animate.css" rel="stylesheet" />

    <!-- JQuery DataTable Css -->
    <link href="http://localhost/savvy/plugins/jquery-datatable/skin/bootstrap/css/dataTables.bootstrap.css" rel="stylesheet">

    <!-- Custom Css -->
    <link href="http://localhost/savvy/css/style.css" rel="stylesheet">

    <!-- AdminBSB Themes. You can choose a theme from css/themes instead of get all themes -->
    <link href="http://localhost/savvy/css/themes/all-themes.css" rel="stylesheet" />
</head>

<body class="theme-red">
<!-- Page Loader -->
    <div class="page-loader-wrapper">
        <div class="loader">
            <div class="preloader">
                <div class="spinner-layer pl-red">
                    <div class="circle-clipper left">
                        <div class="circle"></div>
                    </div>
                    <div class="circle-clipper right">
                        <div class="circle"></div>
                    </div>
                </div>
            </div>
            <p>Please wait...</p>
        </div>
    </div>
    <!-- #END# Page Loader -->
    <!-- Overlay For Sidebars -->
    <div class="overlay"></div>
    <!-- #END# Overlay For Sidebars -->
    <!-- Search Bar -->
    <div class="search-bar">
        <div class="search-icon">
            <i class="material-icons">search</i>
        </div>
        <input type="text" placeholder="START TYPING...">
        <div class="close-search">
            <i class="material-icons">close</i>
        </div>
    </div>
    <!-- #END# Search Bar -->
    <!-- Top Bar -->
    <nav class="navbar">
        <div class="container-fluid">
            <div class="navbar-header">
                <a href="javascript:void(0);" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar-collapse" aria-expanded="false"></a>
                <a href="javascript:void(0);" class="bars"></a>
                <a class="navbar-brand" href="../../index.html">ADMINBSB - MATERIAL DESIGN</a>
            </div>
            <div class="collapse navbar-collapse" id="navbar-collapse">
                <ul class="nav navbar-nav navbar-right">
                    <!-- Call Search -->
                    <li><a href="javascript:void(0);" class="js-search" data-close="true"><i class="material-icons">search</i></a></li>
                    <!-- #END# Call Search -->
                    <!-- Notifications -->
                    <li class="dropdown">
                        <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" role="button">
                            <i class="material-icons">notifications</i>
                            <span class="label-count">7</span>
                        </a>
                        <ul class="dropdown-menu">
                            <li class="header">NOTIFICATIONS</li>
                            <li class="body">
                                <ul class="menu">
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-light-green">
                                                <i class="material-icons">person_add</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4>12 new members joined</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 14 mins ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-cyan">
                                                <i class="material-icons">add_shopping_cart</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4>4 sales made</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 22 mins ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-red">
                                                <i class="material-icons">delete_forever</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>Nancy Doe</b> deleted account</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 3 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-orange">
                                                <i class="material-icons">mode_edit</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>Nancy</b> changed name</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 2 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-blue-grey">
                                                <i class="material-icons">comment</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>John</b> commented your post</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 4 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-light-green">
                                                <i class="material-icons">cached</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4><b>John</b> updated status</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> 3 hours ago
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <div class="icon-circle bg-purple">
                                                <i class="material-icons">settings</i>
                                            </div>
                                            <div class="menu-info">
                                                <h4>Settings updated</h4>
                                                <p>
                                                    <i class="material-icons">access_time</i> Yesterday
                                                </p>
                                            </div>
                                        </a>
                                    </li>
                                </ul>
                            </li>
                            <li class="footer">
                                <a href="javascript:void(0);">View All Notifications</a>
                            </li>
                        </ul>
                    </li>
                    <!-- #END# Notifications -->
                    <!-- Tasks -->
                    <li class="dropdown">
                        <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" role="button">
                            <i class="material-icons">flag</i>
                            <span class="label-count">9</span>
                        </a>
                        <ul class="dropdown-menu">
                            <li class="header">TASKS</li>
                            <li class="body">
                                <ul class="menu tasks">
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Footer display issue
                                                <small>32%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-pink" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 32%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Make new buttons
                                                <small>45%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-cyan" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 45%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Create new dashboard
                                                <small>54%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-teal" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 54%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Solve transition issue
                                                <small>65%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-orange" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 65%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                    <li>
                                        <a href="javascript:void(0);">
                                            <h4>
                                                Answer GitHub questions
                                                <small>92%</small>
                                            </h4>
                                            <div class="progress">
                                                <div class="progress-bar bg-purple" role="progressbar" aria-valuenow="85" aria-valuemin="0" aria-valuemax="100" style="width: 92%">
                                                </div>
                                            </div>
                                        </a>
                                    </li>
                                </ul>
                            </li>
                            <li class="footer">
                                <a href="javascript:void(0);">View All Tasks</a>
                            </li>
                        </ul>
                    </li>
                    <!-- #END# Tasks -->
                    <li class="pull-right"><a href="javascript:void(0);" class="js-right-sidebar" data-close="true"><i class="material-icons">more_vert</i></a></li>
                </ul>
            </div>
        </div>
    </nav>
    <!-- #Top Bar -->
    <section>
        <!-- Left Sidebar -->
        <aside id="leftsidebar" class="sidebar">
            <!-- User Info -->
            <div class="user-info">
                <div class="image">
                    <img src="../../images/user.png" width="48" height="48" alt="User" />
                </div>
                <div class="info-container">
                    <div class="name" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">John Doe</div>
                    <div class="email">john.doe@example.com</div>
                    <div class="btn-group user-helper-dropdown">
                        <i class="material-icons" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">keyboard_arrow_down</i>
                        <ul class="dropdown-menu pull-right">
                            <li><a href="javascript:void(0);"><i class="material-icons">person</i>Profile</a></li>
                            <li role="seperator" class="divider"></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">group</i>Followers</a></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">shopping_cart</i>Sales</a></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">favorite</i>Likes</a></li>
                            <li role="seperator" class="divider"></li>
                            <li><a href="javascript:void(0);"><i class="material-icons">input</i>Sign Out</a></li>
                        </ul>
                    </div>
                </div>
            </div>
            <!-- #User Info -->
            <!-- Menu -->
            <div class="menu">
                <ul class="list">
                    <li class="header">MAIN NAVIGATION</li>
                    <li><a href=""><i class="material-icons">home</i>
                        <span>Home</span></a>
                    </li>
                    <li class="active">
                        <a href="javascript:void(0);" class="menu-toggle">
                            <i class="material-icons">pie_chart</i>
                            <span>Data</span>
                        </a>
                        <ul class="ml-menu">
                            <li>
                                <a href="#">Data Hari Ini</a>
                            </li>
                            <li class="active">
                                <a href="#">History</a>
                            </li>
                        </ul>
                    </li>
                    
                </ul>
            </div>
            <!-- #Menu -->
            <!-- Footer -->
            <div class="legal">
                <div class="copyright">
                    &copy; 2016 <a href="javascript:void(0);">AdminBSB - Material Design</a>.
                </div>
                <div class="version">
                    <b>Version: </b> 1.0.4
                </div>
            </div>
            <!-- #Footer -->
        </aside>
        <!-- #END# Left Sidebar -->
        
    </section>

    <section class="content">
        <div class="container-fluid">
            <div class="block-header">
                <h2>
                    History Data
                   
                </h2>
            </div>
            
            <!-- Exportable Table -->
            <div class="row clearfix">
                <div class="col-lg-12 col-md-12 col-sm-12 col-xs-12">
                    <div class="card">
                        <div class="header">
                            <h2>
                                History
                            </h2>
                            <ul class="header-dropdown m-r--5">
                                <li class="dropdown">
                                    <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
                                        <i class="material-icons">more_vert</i>
                                    </a>
                                    <ul class="dropdown-menu pull-right">
                                        <li><a href="javascript:void(0);">Action</a></li>
                                        <li><a href="javascript:void(0);">Another action</a></li>
                                        <li><a href="javascript:void(0);">Something else here</a></li>
                                    </ul>
                                </li>
                            </ul>
                        </div>
                        <div class="body">
                            <div class="table-responsive">
                                <table class="table table-bordered table-striped table-hover dataTable js-exportable">
                                    <thead>
                                        <tr>
                                            <th>No</th>
                                            <th>Suhu</th>
                                            <th>Datetime</th>
                                        </tr>
                                    </thead>
                                    <tfoot>
                                        <tr>
                                            <th>No</th>
                                            <th>Suhu</th>
                                            <th>Datetime</th>
                                        </tr>
                                    </tfoot>
                                    <tbody>
    <?php
    $no=1;
    $stmt = $DB_con->prepare('SELECT * FROM temps ORDER BY id');
    $stmt->execute();
    
    if($stmt->rowCount() > 0)
    {
        while($row=$stmt->fetch(PDO::FETCH_ASSOC))
        {
            extract($row);
            ?>
          <tr>
            <th scope="row"><?php echo $no++; ?></th>
            <td><?php echo $temp; ?></td>
            <td><?php echo $day; ?></td>
          </tr>
<?php
        }
    }
    else
    {
        ?>
          <td colspan="3">No Data Found ...</td>
            
        <?php
    }
  ?>
                                        
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- #END# Exportable Table -->
        </div>
    </section>

    <!-- Jquery Core Js -->
    <script src="http://localhost/savvy/plugins/jquery/jquery.min.js"></script>

    <!-- Bootstrap Core Js -->
    <script src="http://localhost/savvy/plugins/bootstrap/js/bootstrap.js"></script>

    <!-- Select Plugin Js -->
    <script src="http://localhost/savvy/plugins/bootstrap-select/js/bootstrap-select.js"></script>

    <!-- Slimscroll Plugin Js -->
    <script src="http://localhost/savvy/plugins/jquery-slimscroll/jquery.slimscroll.js"></script>

    <!-- Waves Effect Plugin Js -->
    <script src="http://localhost/savvy/plugins/node-waves/waves.js"></script>

    <!-- Jquery DataTable Plugin Js -->
    <script src="http://localhost/savvy/plugins/jquery-datatable/jquery.dataTables.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/skin/bootstrap/js/dataTables.bootstrap.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/dataTables.buttons.min.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/buttons.flash.min.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/jszip.min.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/pdfmake.min.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/vfs_fonts.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/buttons.html5.min.js"></script>
    <script src="http://localhost/savvy/plugins/jquery-datatable/extensions/export/buttons.print.min.js"></script>

    <!-- Custom Js -->
    <script src="http://localhost/savvy/js/admin.js"></script>
    <script src="http://localhost/savvy/js/pages/tables/jquery-datatable.js"></script>

    <!-- Demo Js -->
    <script src="http://localhost/savvy/js/demo.js"></script>
</body>

</html>
```

**Suhu.sql**
```
-- phpMyAdmin SQL Dump
-- version 4.5.1
-- http://www.phpmyadmin.net
--
-- Host: 127.0.0.1
-- Generation Time: Aug 10, 2017 at 10:54 AM
-- Server version: 10.1.10-MariaDB
-- PHP Version: 5.6.19

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `thermometer`
--

-- --------------------------------------------------------

--
-- Table structure for table `temps`
--

CREATE TABLE `temps` (
  `id` int(11) NOT NULL,
  `temp` int(11) NOT NULL,
  `day` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Dumping data for table `temps`
--

INSERT INTO `temps` (`id`, `temp`, `day`) VALUES
(1, 30, '2017-08-01 02:24:49'),
(2, 31, '2017-08-01 03:03:07'),
(3, 30, '2017-08-01 04:13:29'),
(4, 30, '2017-08-02 04:13:29'),
(5, 32, '2017-08-03 04:13:29'),
(6, 31, '2017-08-03 04:13:29'),
(7, 30, '2017-08-06 04:13:29'),
(8, 31, '2017-08-06 04:13:29'),
(9, 30, '2017-08-07 04:13:29'),
(10, 30, '2017-08-07 04:13:29'),
(11, 31, '2017-08-07 04:13:29'),
(12, 30, '2017-08-07 04:13:29'),
(13, 31, '2017-08-09 04:13:29'),
(14, 31, '2017-08-09 04:13:29'),
(15, 30, '2017-08-09 04:13:29'),
(16, 30, '2017-08-09 04:13:29'),
(17, 32, '2017-08-09 04:13:29'),
(18, 31, '2017-08-09 04:13:29'),
(19, 32, '2017-08-09 04:13:29'),
(20, 33, '2017-08-09 04:13:29'),
(21, 33, '2017-08-09 04:13:29');

--
-- Indexes for dumped tables
--

--
-- Indexes for table `temps`
--
ALTER TABLE `temps`
  ADD PRIMARY KEY (`id`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `temps`
--
ALTER TABLE `temps`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=22;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
```

**dbconfig.php**
```
<?php

	$DB_HOST = 'localhost';
	$DB_USER = 'root';
	$DB_PASS = '';
	$DB_NAME = 'suhu';
	
	try{
		$DB_con = new PDO("mysql:host={$DB_HOST};dbname={$DB_NAME}",$DB_USER,$DB_PASS);
		$DB_con->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
	}
	catch(PDOException $e){
		echo $e->getMessage();
	}
?>
```

Project ini selengkapnya dapat dilihat di [https://dirakit.hackster.io/brianrakhmat/savvy-home-mengontrol-suhu-sederhana-menggunakan-php-mysql-fa4b6c?ref=channel&ref_id=43423_trending___&offset=1](https://dirakit.hackster.io/brianrakhmat/savvy-home-mengontrol-suhu-sederhana-menggunakan-php-mysql-fa4b6c?ref=channel&ref_id=43423_trending___&offset=1)