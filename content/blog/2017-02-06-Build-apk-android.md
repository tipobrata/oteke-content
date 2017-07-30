+++
title = "Ionic to Apk=Android"
date = "2017-02-06T21:49:20+02:00"
tags = ["ionic"]
categories = ["Ionic"]
author = "tipobrata"
+++

## Start
Belajar ionic dan membuild ionic ke apk sehingga bisa di gunakan pada android

## Memasang AndroidSDK
Download terlebih dahulu[AndroidSdk](https://dl.google.com/android/repository/tools_r25.2.3-windows.zip) sesuai OS
 
Pasang Path di windows, Buat variabel di bawah: 
```
Variabel Name: ANDROID_HOME 
Variabel Value: D:\Tools\android_sdk\tools;D:\Tools\android_sdk\platform-tools
```

Jalankan di cmd :

```
set ANDROID_HOME=D:\Tools\android_sdk
set PATH=%PATH%;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools
```

Download versi/API Android `dari yang bawah dan yang tertinggi.`
contoh: 4.0(API 14) dan 7.1(API 25)

//Optional Install
- [apache ant](http://mirror.wanxp.id/apache//ant/binaries/apache-ant-1.9.7-bin.zip)

## MEMBUAT APPLIKASI MOBIL DENGAN ANGULAR 2 DAN IONIC 2

Tools yang di butuhkan :

- $ npm install -g cordova
- $ npm install -g ionic
- $ npm install -g typescript
- $ npm install -g typings

- $ npm cache clean //clear cache instalasi
- $ reactive-native init

- Jika Gagal

    Note: Jika error pada ionic-cli jalankan uninstall `npm uninstall -g ionic`, cara clear cache instalasi npm, gunakan perintah `npm cache clean` dan install ionic-cli dengan perintah `npm install -g ionic`

Jalankan perintah `ionic info`

```
            ******************************************************
             Dependency warning - for the CLI to run correctly,
             it is highly recommended to install/upgrade the following:

             Please install your Cordova CLI to version  >=4.2.0 `npm install -g cordova`

            ******************************************************

            Your system information:

             You have been opted out of telemetry. To change this, run: cordova telemetry on
            .
            6.4.0

            Ionic CLI Version: 2.1.17
            Ionic App Lib Version: 2.1.7
            ios-deploy version: Not installed
            ios-sim version: Not installed
            OS: Windows 7
            Node Version: v6.9.1
            Xcode version: Not installed


            ******************************************************
```

## MEMBUAT PROJECT IONIC (jalankan di cmd)

- $ ionic start githubIonic tutorial --v2
- $ cd githubIonic
- $ ionic serve

```  
        [15:45:51]  ionic-app-scripts 0.0.47
        [15:46:07]  watch started ...
        [15:46:07]  build dev started ...
        [15:46:07]  clean started ...
        [15:46:07]  clean finished in 2 ms
        [15:46:07]  copy started ...
        [15:46:07]  transpile started ...
        [15:46:35]  transpile finished in 28.07 s
        [15:46:35]  webpack started ...
        [15:46:38]  copy finished in 31.22 s
        [15:47:03]  webpack finished in 27.71 s
        [15:47:03]  sass started ...
        [15:47:09]  sass finished in 5.99 s
        [15:47:09]  build dev finished in 61.98 s
        [15:47:11]  watch ready in 63.99 s
        [15:47:11]  dev server running: http://localhost:8100/
```
- Buka http://localhost:8100/

## Install packages yang di butuhkan : 

- $ npm install @ionic/app-scripts@latest --save-dev                //install @ionic/app-scripts terbaru
- $ npm install @types/request@0.0.30 --save-dev --save-exact
- $ npm install @types/jasmine@2.5.36 --save-dev --save-exact       //install dependency firebase
- $ npm install firebase angularfire2 --save

## Menambah platform android pada folder project anda

```
$ ionic platform add android
```

```
$ ionic build android
```

This builds the application, and puts the built apk in the `platforms/android/build/outputs` folder.

## Run the android app

```
 $ ionic run android
```

## Hapus platform Android

```
ionic platform rm android
```


## Langkah jika error

```
$ npm install -g gradle
$ ionic platform rm android
$ ionic platform add android
$ ionic build android
```

## Membuat APK
Setelah menjalankan perintah `ionic build android`, pada baris terakhir akan muncul tampilan di bawah : `android-debug.apk` merupakan apk yang bisa kita install di android.

```
BUILD SUCCESSFUL
Total time: 2 mins 43.35 secs
Built the following apk(s):
D:/Tools/Tutorial-Ionic/bloggerfire/platforms/android/build/outputs/apk/android-debug.apk
```

```
$ cordova platforms ls
Installed platforms:
  android 6.1.2
Available platforms:
  amazon-fireos ~3.6.3 (deprecated)
  blackberry10 ~3.8.0
  browser ~4.1.0
  firefoxos ~3.6.3
  webos ~3.7.0
  windows ~4.4.0
  wp8 ~3.8.2 (deprecated)
```

## IOS

```
$ npm install -g ios-deploy
$ npm install -g ios-sim version
```

```
 $ ionic platform add ios
```

## Build App IOS

```
$ ionic build ios
```

This builds the application, and puts the build output in the `platforms/ios/build/emulator` folder.

Then run the application in an ios simulator that comes installed with xCode
```
 $ ionic run ios
```

## Path Environment pada windows
```
C:\ProgramData\Oracle\Java\javapath;%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;C:\Windows\System32;%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\;C:\Program Files\Heroku\bin;C:\Program Files\git\cmd;D:\Tools\nodejs\;D:\Tools\Python27;D:\Tools\Python27\Scripts;C:\Program Files\Java\jdk1.8.0_92\bin;D:\J2EE\apache-maven-3.3.9\bin;C:\Program Files\MySQL\MySQL Utilities 1.6\;C:\Program Files\Git\cmd;D:\Tools\android-sdk\tools;D:\Tools\android-sdk\;%ANT_HOME%\bin;C:\Program Files\MySQL\MySQL Fabric 1.5.4 & MySQL Utilities 1.5.4 1.5\;C:\Program Files\MySQL\MySQL Fabric 1.5.4 & MySQL Utilities 1.5.4 1.5\Doctrine extensions for PHP\
```