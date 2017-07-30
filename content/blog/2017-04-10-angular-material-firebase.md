+++
title = "Angular-material dan Firebase"
date = "2017-03-10T21:49:20+02:00"
tags = ["angular", "material", "angularFire2"]
categories = ["angular", "material"]
author = "tipobrata"
+++

# Menggunakan Material pada Angular
[material-angular](https://material.angular.io/)

## List Array Pada Firebase

**Buat project Angular**

```
$ ng new fireMaterial
$ cd fireMaterial
```

**Install Material dalam folder project**

```
npm install --save @angular/material
```

**Install Module Angular Animation**

```
npm install --save @angular/animations
```

**Pada `app.module.ts`, import code di bawah:**

```
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';
import { MaterialModule, MdButtonModule, MdCheckboxModule} from '@angular/material';
```

**dan**

```
  imports: [
    MaterialModule,
    BrowserAnimationsModule,
    MdButtonModule,
    MdCheckboxModule
  ],
```

**Memsasang Theme material, Buka `index.html` pada root folder copy code di bawah :**

```
<link href="../node_modules/@angular/material/prebuilt-themes/indigo-pink.css" rel="stylesheet">
```

**Memasang Icon Material, Buka `index.html` pada root folder copy code di bawah :**

```
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```

>Gesture: tambahkan `hammerJs` ke dalam folder project, jika kita akan 
menggunakan beberapa components seperti (md-slide-toggle, md-slider, mdTooltip) menggunakan HammerJS untuk gestures.*

**Install hammerJS**

```
npm install --save hammerjs
```

**Setelah installing, import pada app's root module.**

```
import 'hammerjs';
```

**Buka file `.angular-cli.json`, edit bagian di bawah :**

```
"styles": [
        "styles.css"
      ],
```

**Menjadi**

```
"styles": [
        "styles.scss"
      ],
```

**lakukan Hal yang sama**

```
"defaults": {
    "styleExt": "css",
    "component": {}
  }
```

**Menjadi**

```
"defaults": {
    "styleExt": "scss",
    "component": {}
  }
```

**Define SCSS, jika meggunakan scss buat file `style.scss` dan copy kode di bawah(jangan lupa hapus terlebih daulu file style.css):**

```
@import '~@angular/material/theming';
// Plus imports for other components in your app.

// Include the base styles for Angular Material core. We include this here so that you only
// have to load a single css file for Angular Material in your app.
@include mat-core();

// Define the palettes for your theme using the Material Design palettes available in palette.scss
// (imported above). For each palette, you can optionally specify a default, lighter, and darker
// hue.
$candy-app-primary: mat-palette($mat-indigo);
$candy-app-accent:  mat-palette($mat-pink, A200, A100, A400);

// The warn palette is optional (defaults to red).
$candy-app-warn:    mat-palette($mat-red);

// Create the theme object (a Sass map containing all of the palettes).
$candy-app-theme: mat-light-theme($candy-app-primary, $candy-app-accent, $candy-app-warn);

// Include theme styles for core and each component used in your app.
// Alternatively, you can import and @include the theme mixins for each component
// that you are using.
.app-primary{
@include angular-material-theme($candy-app-theme);
}

```


**Selanjutnya buka file `app.component.html` copy code di bawah :**

```
<md-sidenav-container class="app-primary">

    <md-sidenav #sidenav mode="side" class="app-sidenav">
        Sidenav
    </md-sidenav>

    <md-toolbar color="primary">
        <button class="app-icon-button" (click)="sidenav.toggle()">
      <i class="material-icons app-toolbar-menu">menu</i>
    </button> Angular Material2 Example App

        <span class="app-toolbar-filler"></span>
        <button md-button (click)="isDarkTheme = !isDarkTheme">TOGGLE DARK THEME</button>
    </md-toolbar>

    <div class="app-content">
        Ini adalah Contetnt
    </div>

</md-sidenav-container>
<span class="app-action" [class.m2app-dark]="isDarkTheme">
  <button md-fab><md-icon>check circle</md-icon></button>
</span>
```

**Untuk merubah warna buka file style.scss dan copy kode di bawah:**

```
$candy-app-primary: mat-palette($mat-light-green);
$candy-app-accent: mat-palette($mat-light-green, A200, A100, A400);
```

**Install AngularFire2 ke dalam folder project**

```
npm install firebase angularfire2 --save
```

**Buka `app.module.ts` import module di bawah:**

```
import { AngularFireModule, AuthProviders, AuthMethods } from 'angularfire2';
```

**Import api key dr firebase:**

```
export const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    databaseURL: "",
    storageBucket: "",
    messagingSenderId: ""
};
```

**Import config agar bisa login menggunakan account google.**

```
const fbAuthConfig = {
  provider: AuthProviders.Google,
  method: AuthMethods.Password
};
```

**Import pada NgModule**

```
imports: [
AngularFireModule.initializeApp(firebaseConfig, fbAuthConfig),
],
```

> Buka `app.component.ts` import module berikut

```
import { AngularFire, FirebaseListObservable } from 'angularfire2';
```

> Tambahkan pada constructor module angularfire

```
constructor(private af: AngularFire){
}
```

> Buat databse di `firebase console` buat collection/database dengan nama `tweets`

> Buka `app.component.html` untuk menampilkan array `message` dengan menggunakan `*ngFor` menggunakan class `FirebaseListObservable` berikut codenya:

```
<div class="app-content">
        <ul>
            <li class="text" *ngFor="let item of items | async">
                <a>{{item.message}}</a>
            </li>
        </ul>
</div>
```

> Buka `app.component.ts` dan tambahkan kode di bawah

> Di atas constructor definisikan `FirebaseListObservable<any[]>`

```
items: FirebaseListObservable<any[]>;
```

> dan di dalam constructor tambahkan kode di bawah: 

```
this.items = af.database.list('/tweets');
```

Ket:

- `af`: definisi/config firebase  yang di pasang pada contructor.

- `database`: class database

- `list`: menggunakan method dari `FirebaseListObservable` yaitu untuk menampilkan array pada table atau collection.

- `tweets`: nama table yang sudah di buat di firebase


## Login dan Register

**user.model.ts**
Buat file `user.model.ts` yang ada dalam folder `app/model`

```
export class User {
    public id?:string;
    public firstName?:string;
    public lastName?:string;
    public email?:string;
    public password?:string;
    public avatar?:string;
}
```

**Isi file `firebase.service.ts`**

```
import { Injectable } from '@angular/core';
import { AngularFire, FirebaseListObservable } from 'angularfire2';
import { MdDialog } from '@angular/material';
import { AppComponent } from '../app.component';
import { LoginComponent } from '../users/login/login.component';

@Injectable()
export class FirebaseService {
  
  tweet: FirebaseListObservable<any[]>
  constructor(private af: AngularFire, private dialog: MdDialog) { }

    getTweets(){
    this.tweet = this.af.database.list('/tweets') as
    FirebaseListObservable<Tweets[]>
    return this.tweet;
    }
}

interface Tweets{
   $key?: string;
   $message?: string;
}

```


**Login**

Isi File `login.component.ts`

```
import { Component, OnInit } from '@angular/core';
//import { FirebaseService } from '../../services/firebase.service';
import { User } from '../../models/user.model';
import { AngularFire, FirebaseListObservable } from 'angularfire2';
import { MdDialogRef, MdDialog } from '@angular/material';
import {RegisterComponent} from '../register/register.component';


@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.scss']
})
export class LoginComponent implements OnInit {

  private user: User = new User();
  message: string;
  constructor(private dialogRef: MdDialogRef<LoginComponent>, private af: AngularFire, private dialog: MdDialog) {
    this.af.auth.subscribe(auth => {
      if(auth){
        this.dialogRef.close();
      }
    });
   }

  ngOnInit() {
  }

  onLogin(){
    if(!this.user.email || !this.user.password){
      this.message = "Email dan Password Salah";
      return;
    }
    let data = {
      email: this.user.email,
      password: this.user.password,
    };
    //console.log("User data:", this.user);
    this.af.auth.login(data);
  }

  register(){
    this.dialogRef.close();
    this.dialog.open(RegisterComponent, {
        width: '500px'
    });
  }
}

```

Isi File `login.component.html`

```
<form #f="ngForm" (ngSubmit)="onLogin()">
    <div class="message">
        <p>{{message}}</p>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="email" name="email" placeholder="Email" [(ngModel)]="user.email" />
        </md-input-container>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="password" name="password" placeholder="Password" [(ngModel)]="user.password" />
        </md-input-container>
    </div>
    <div class="form-group">
        <button md-raised-button color="default" type="submit">Login</button> Or <button md-button type="button" (click)="register()">Register</button>
    </div>
</form>
```


**Register**
berikut isi file `register.component.ts`

```
import { Component, OnInit } from '@angular/core';
import { User } from '../../models/user.model';
import { AngularFire, FirebaseListObservable } from 'angularfire2';
import { MdDialogRef } from '@angular/material';

@Component({
  selector: 'app-register',
  templateUrl: './register.component.html',
  styleUrls: ['./register.component.scss']
})
export class RegisterComponent implements OnInit {

  user: User = new User();
  message: string;
  constructor(private af: AngularFire, private dialogRef: MdDialogRef<RegisterComponent>) { 

    this.af.auth.subscribe(auth => {
      if(auth){
        this.dialogRef.close();
        let userId = auth.uid;
        const user = this.af.database.object('/users/'+userId);
        let userData = {
          firstName: this.user.firstName,
          lastName: this.user.lastName,
          avatar: this.user.avatar,
        };
        user.set(userData);
      }
  });
  }

  ngOnInit() {
  }

  onRegister(){
    //console.log(this.user);

    let data = {
      email: this.user.email,
      password: this.user.password
    }

    this.af.auth.createUser(data);
  }

}

```

Berikut isi file `register.component.html`

```
<form #f="ngForm" (ngSubmit)="onRegister()">
    <div class="message">
        <p>{{message}}</p>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="text" name="firstName" placeholder="First Name" [(ngModel)]="user.firstName" />
        </md-input-container>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="text" name="lastName" placeholder="Last Name" [(ngModel)]="user.lastName" />
        </md-input-container>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="text" name="avatar" placeholder="Avatar Url" [(ngModel)]="user.avatar" />
        </md-input-container>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="email" name="email" placeholder="Email" [(ngModel)]="user.email" />
        </md-input-container>
    </div>
    <div class="form-group">
        <md-input-container class="full-width">
            <input mdInput type="password" name="password" placeholder="Password" [(ngModel)]="user.password" />
        </md-input-container>
    </div>
    <div class="form-group">
        <button md-raised-button color="default" type="submit">Register</button>
    </div>
</form>
```

## File Upload

Pada `register.component.ts` rubah pada seperti code di bawah.

```
constructor(private af: AngularFire, private dialogRef: MdDialogRef<RegisterComponent>) { 

    this.af.auth.subscribe(auth => {
      if(auth){
        this.dialogRef.close();
        let userId = auth.uid;
        const user = this.af.database.object('/users/'+userId);
        let userData = this.user;
        delete userData.password;
        user.set(userData);
      }
  });
  }
```


Menambahkan field `created` pada table `users` di firebase

pada `user.model.ts` tambahkan kode di bawah :

```
public created?:any;
```

Tambahkan import di bawah pada `register.component.ts`
```
import * as firebase from 'firebase';
```

Tambahkan kode di bawah untuk menampilkan `timestamp`

```
userData.created = firebase.database.ServerValue.TIMESTAMP;
```

lakukan register ulang

Menampilkan Avatar
Buat terlebih dahulu component avatar

```
ng  g component shared/avatar
```

Setelah di buat kita akan menampilkan avatar pada modal register

edit `register.component.html` dan tambahkan kode di bawah:

```
<div class="form-group form-avatar-control">
//selector dari component avatar
<avatar></avatar>
</div>
```

edit `avatar.component.html` untuk membuat input file gambar:

```
<input type="file" name="file" #fileInput (change)="handleUpload($event, fileInput)" />
```

testing dengan console.log buat function `handleUpload` ketikkan functionnya di bawah :

```
handleUpload(e: any, input: any): void{
    console.log("file object",input.files[0]);
  }
```



## Script Google Analytic:

```
<body>
  <material2-app-app>Loading...</material2-app-app>

  <script>
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    ga('create', 'nomor_di_isi', 'auto');
    ga('send', 'pageview');
  </script>
</body>
```
