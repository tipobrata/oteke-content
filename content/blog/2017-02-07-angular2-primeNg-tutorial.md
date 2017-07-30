+++
title = "Angular dan PrimeNg"
date = "2017-02-07T21:49:20+02:00"
tags = ["angular", "PrimeNg", "angularFire2"]
categories = ["angular"]
author = "tipobrata"
+++

## Buat Project dengan angular2-cli

```
$ ng new angularprimetutorial
installing ng2
  create .editorconfig
  create README.md
  create src\app\app.component.css
  create src\app\app.component.html
  create src\app\app.component.spec.ts
  create src\app\app.component.ts
  create src\app\app.module.ts
  create src\assets\.gitkeep
  create src\environments\environment.prod.ts
  create src\environments\environment.ts
  create src\favicon.ico
  create src\index.html
  create src\main.ts
  create src\polyfills.ts
  create src\styles.css
  create src\test.ts
  create src\tsconfig.json
  create angular-cli.json
  create e2e\app.e2e-spec.ts
  create e2e\app.po.ts
  create e2e\tsconfig.json
  create .gitignore
  create karma.conf.js
  create package.json
  create protractor.conf.js
  create tslint.json
Successfully initialized git.
Installing packages for tooling via npm.
Installed packages for tooling via npm.
Project 'angularprimetutorial' successfully created.
$ cd angularprimetutorial
```

* Install UI-PrimeNg

```
$ npm install primeng --save
angularprimetutorial@0.0.0 D:\Tools\Tutorial-Angular\angularprimetutorial
`-- primeng@2.0.0-rc.3
```

* Jalankan

```
$ npm start
> angularprimetutorial@0.0.0 start D:\Tools\Tutorial-Angular\angularprimetutorial
> ng serve

fallbackLoader option has been deprecated - replace with "fallback"
loader option has been deprecated - replace with "use"
fallbackLoader option has been deprecated - replace with "fallback"
loader option has been deprecated - replace with "use"
fallbackLoader option has been deprecated - replace with "fallback"
loader option has been deprecated - replace with "use"
fallbackLoader option has been deprecated - replace with "fallback"
loader option has been deprecated - replace with "use"
** NG Live Development Server is running on http://localhost:4200. **
Hash: 29ffb5b4a31846691750
Time: 28261ms
chunk    {0} main.bundle.js, main.bundle.map (main) 4.69 kB {2} [initial] [rendered]
chunk    {1} styles.bundle.js, styles.bundle.map (styles) 9.96 kB {3} [initial] [rendered]
chunk    {2} vendor.bundle.js, vendor.bundle.map (vendor) 2.83 MB [initial] [rendered]
chunk    {3} inline.bundle.js, inline.bundle.map (inline) 0 bytes [entry] [rendered]
webpack: Compiled successfully.
```

* Tambahkan baris di bawah untuk file `D:\Tools\Tutorial-Angular\angularprimetutorial\src\index.html`

```
<link rel="stylesheet" type="text/css" href="styles.css">
```

* Pasang CSS dan Themes bawaan primeNg `D:\Tools\Tutorial-Angular\angularprimetutorial\src\styles.css`

```
@import "../node_modules/primeng/resources/primeng.css";
@import "../node_modules/primeng/resources/themes/omega/theme.css";
```

> Setelah kita membuat strukture dari angular2, saat nya memulai coding membuat tampilan halaman login, di mulai dengan membuat `pages`

## Membuat Pages Login
Buka `D:\Tools\Tutorial-Angular\angularprimetutorial\src\app` buat folder `pages\login.component.html` dan `pages\login.component.ts`

Isi file `login.component.html`  kode di bawah :
```
{{titlelogin}}
```
Isi file `login.component.ts`  kode di bawah :

```
import {Component} from '@angular/core';

@Component({
    templateurl: './login.component.html'
})
export class LoginComponent {
    private titlelogin: string = 'login work';
}
```

Buka pada `app.module.ts` *D:\Tools\Tutorial-Angular\angularprimetutorial\src\app\app.module.ts* di bawah `import { AppComponent } from './app.component';` tambahkan

```
import { LoginComponent } from './pages/login.component';
```

Buat `app.routes.ts` di dalam folder *src/app* isi dengan kode di bawah :

```
import { ModuleWithProviders } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { LoginComponent } from "./pages/login/login.component";

export const routes: Routes = [
    {
        path: '',
        redirectTo: 'login',
        pathMatch: 'full'
    },
    {
        path: 'login',
        component: LoginComponent
    }
];
export const RoutingModule: ModuleWithProviders = RouterModule.forRoot(routes);
```

pada `app.module.ts` edit kode menjadi seperti bawah :

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';
import { LoginComponent } from "./pages/login/login.component";

import {RoutingModule} from './app.routes';

@NgModule({
  declarations: [
    AppComponent,
    LoginComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    RoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

pada `app.component.html` edit kode menjadi seperti bawah :

```
<router-outlet></router-outlet>
```

> #LANGKAH 2

Kita akan memulai mendesain halaman utama menjadi yaitu tampilan username dan password. 
[ref primeNg](http://www.primefaces.org/primeng/#/inputtext)

pada `style.css`
```
.main_content {
    text-align: center;
    font-size: 25px;
    margin-top: 40px;
}

hr {
    height: 0px;
    visibility: hidden;
}
```

Pada `app.module.ts` tambahkan import modul di bawah.

```
// Component primeng
import {InputTextModule} from 'primeng/primeng';
```

Jangan lupa Tambahkan juga pada baris import setelah `RoutingModule,`
```
InputTextModule
```

Edit file `login.component.html` menjadi seperti di bawah : 
```
<div class="main_content">
    <span>Username</span>
    <hr/>
    <input type="username" pInputText [(ngModel)]="username" />
    <hr/>
    <span>Password</span>
    <hr/>
    <input type="password" pInputText [(ngModel)]="password" />
    <hr/>
</div>
```

Pada `login.component.ts` pasang variabel username dan password tambahkan kode di bawah pada class ` `.

```
export class LoginComponent {
    private username: string;
    private username: string;

    public login(): void {
        alert("Saya Sedang login");
    }
}
```

## Membuat Tombol Button

Tambahkan juga pada `app.module.ts`  untuk modul button di bawah.
```
import { InputTextModule, ButtonModule } from 'primeng/primeng';
```

Jangan lupa Tambahkan juga pada baris import setelah `InputTextModule,`
```
ButtonModule
```

tambahkan pada `login.component.html`
```
<button pButton type="button" (click)="login()" label="GO"></button>
```

`(click)="login()` : Jika di klik akan muncul alert "Saya sedang Login" merupakan fungsi `login()` yang sudah kita buat di class `LoginComponent` pada `login.component.ts`

Buat 3 folder di bawah di dalam folder `app` :
 - `model\user.model.ts`
 - `mock\user.mock.ts`
 - `services\auth.service.ts`

## Mendefinisikan username dan password

Buka `user.model.ts` Mendefinisikan username dan password
```
export interface User {
    username: string,
    password: string
}
```

## Menyimpan konfigurasi username dan password

Buka `user.mock.ts` untuk Menyimpan konfigurasi username dan password
```
import {User} from '../model/user.model';

export const USER: User = {
    username: 'admin',
    password: 'admin'
};

```

* Buka `auth.service.ts` untuk mendefinisikan username dan password saat login

```
import { Injectable } from '@angular/core';
import { User } from '../model/user.model';
import { USER } from '../mock/user.mock';

@Injectable()
    export class AuthService {
        login(user: User): Promise<boolean>{
            if(user.username === USER.username && user.password === USER.password) {
                return Promise.resolve(true);
            }else {
                return Promise.resolve(false);
            }
        }
    }
```

Pada `app.module.ts` tambahkan kode di bawah

```
// Services
import { AuthService } from './services/auth.service';
```

dan juga pada baris `providers`

```
providers: [AuthService],
```

## Membuat Message Error Pada Form Login

> Buka `login.component.html` tambahkan kode di bawah di bawah `</div>`

```
<p-growl [value]="msgs"></p-growl>
```

> Buka `app.modul.ts` tambahkan `GrowlModule` untuk baris di bawah 

```
// Component primeng
import { InputTextModule, ButtonModule, GrowlModule } from 'primeng/primeng';
```

dan pada baris import tambahkan `GrowlModule`

```
imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    RoutingModule,
    InputTextModule,
    ButtonModule,
    GrowlModule
  ],
```

> Buka `login.component.ts` pada import dan export class tmbahkan  `private msgs: Message[] = [];`

Tambahkan Import `Message` di bawah
```
import {Message} from 'primeng/primeng';
```

```
export class LoginComponent {
    private username: string;
    private password: string;
    private msgs: Message[] = [];
```

pada baris `elese` tambahkan kode di bawah :

```
else {
      this.msgs.push({severity: 'error', summary: 'Attention', detail: 'Le Credential'});
     }
```

gambar

## Membuat Page Homepage

Buat Folder `homepage` dan isikan 2 file di bawah :
- homepage.component.html
- homepage.component.ts

*homepage.component.ts*
```
import { Component } from '@angular/core';
@Component({
    templateUrl: './homepage.component.html'
})

export class HomepageComponent{
    private titlehomepage: String = "Halaman HomePage";
}
```

*homepage.component.html*

```
{{titlehomepage}}
```

Buka *app.routes.ts*

import `HomepageComponent`
```
import { HomepageComponent } from './pages/homepage/homepage.component';
```

tambahkan `route`

```
{
        path: 'homepage',
        component: HomepageComponent
    }
```

Buka *app.module.ts*

Tambahkan import component `HomepageComponent`

```
import { HomepageComponent } from './pages/homepage/homepage.component';
```

pada `@NgModule` tambahkan dibawah `LoginComponent`

```
HomepageComponent
```

Buka `login.component.ts`

Pada `contructor` tambahkan `private router: Router` seperti di bawah :

```
constructor(private authService: AuthService, private router: Router) {
}
```

pada baris `authService` Tambahkan ` this.router.navigate(['./homepage']);` seperti di bawah :
```
        this.authService.login(user).then((result: boolean) => {
            if (result) {
                this.router.navigate(['./homepage']);
            }else {
                this.msgs.push({severity: 'error', summary: 'Attention', detail: 'Le Credential'});
            }
        })
```

buka `http://localhost:4200/`lakukan test login dengan benar apakah berhasil ?

## ROUTE - SESSION STORAGE. 
yaitu : user yang sudah login tidak bisa keluar jika tidak di logout.

Buat file `utility.service.ts` dalam folder `services` isi dengan code di bawah

```
import { Injectable } from '@angular/core';
@Injectable()

export class UtilityService{
    isLogged(): Promise<boolean> {
        if (typeof (Storage) !== 'undefine') {
            if (sessionStorage.getItem('User')) {
                return Promise.resolve(true);
            }
        }
        return Promise.resolve(false);
    }
}
```

buka `login.component.ts` edit menjadi kode di bawah :

```
import { Component, OnInit } from '@angular/core';
import { User } from '../../model/user.model';
import { AuthService } from '../../services/auth.service';
import { UtilityService } from '../../services/utility.service';

import { Message } from 'primeng/primeng';
import { Router } from '@angular/router';

@Component({
    templateUrl: './login.component.html'
})
export class LoginComponent implements OnInit{
    private username: string;
    private password: string;
    private msgs: Message[] = [];

constructor(private authService: AuthService, private router: Router, private utility: UtilityService) {
}

  ngOnInit(): void {
    this.utility.isLogged().then((result: boolean) => {
        if (result) {
            this.router.navigate(['/homepage']);
        }
    })
}

    public login(): void {
        const user: User = {
            username: this.username,
            password: this.password
        };
        this.authService.login(user).then((result: boolean) => {
            if (result) {
                if (typeof (Storage) !== 'undefined') {
                    sessionStorage.setItem('User', user.username)
                }
                this.router.navigate(['./homepage']);
            }else {
                this.msgs.push({severity: 'error', summary: 'Attention', detail: 'Le Credential'});
            }
        });
    }
}
```

buka `homepage.component.ts` edit menjadi seperti di bawah :

```
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { UtilityService } from '../../services/utility.service';
@Component({
    templateUrl: './homepage.component.html'
})

export class HomepageComponent implements OnInit{
    private titlehomepage: String = "Halaman HomePage";
constructor(private utility: UtilityService, private router: Router){
}
    ngOnInit(): void {
    this.utility.isLogged().then((result: boolean) => {
        if(result){
            this.router.navigate(['/login']);
        }
    })
}
}
```

Buka `app.module.ts` import `UtilityService` dan tambahkan `providers`  `UtilityService` seperti di bawahkode di bawah 

```
import { UtilityService } from './services/utility.service';

-------------------------------------------------------------

providers: [AuthService, UtilityService],

```


## Accordion e Header Component with PrimeFaces

> Buka `app.module.ts` tambahkan `AccordionModule` pada component primeNg dan @NgModule -> import kode lengkap seperti di bawah : 

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';
import { LoginComponent } from './pages/login/login.component';
import { HomepageComponent } from './pages/homepage/homepage.component';

import { RoutingModule } from './app.routes';

// Services
import { AuthService } from './services/auth.service';
import { UtilityService } from './services/utility.service';

// Component primeng
import { InputTextModule, ButtonModule, GrowlModule, AccordionModule } from 'primeng/primeng';

@NgModule({
  declarations: [
    AppComponent,
    LoginComponent,
    HomepageComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    RoutingModule,
    InputTextModule,
    ButtonModule,
    GrowlModule,
    AccordionModule
  ],
  providers: [AuthService, UtilityService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

> buka homepage.component.html

```
<div class="main_content">
    <h1>List Didit</h1>
    <p-accordion (onOpen)="onTabOpen($event)">
        <p-accordionTab header="Godfather I">
            The story begins as Don Vito Corleone, the head of a New York Mafia family, overseeshis daughter's wedding. His beloved son ichael has just come home from the war, but does not intend to become part of his father's business. T hrough Michael's life the
            nature of the family business becomes clear. The business of the family is just like the head of the family, kind and benevolent to those who give respect, but given to ruthless violence whenever anything stands against the good of the family.
            <hr/>
        </p-accordionTab>
        <p-accordionTab header="Godfather II">
            Francis Ford Coppola's legendary continuation and sequel to his landmark 1972 film, The_Godfather parallels the young Vito Corleone's rise with his son Michael's spiritual fall, deepening The_Godfather's depiction of the dark side of the American dream.
            In the early 1900s, the child Vito flees his Sicilian village for America after the local Mafia kills his family. Vito struggles to make a living, legally or illegally, for his wife and growing brood in Little Italy, killing the local Black
            Hand Fanucci after he demands his customary cut of the tyro's business. With Fanucci gone, Vito's communal stature grows.
        </p-accordionTab>
        <p-accordionTab header="Godfather III">
            After a break of more than 15 years, director Francis Ford Coppola and writer Mario Puzo returned to the well for this third and final story of the fictional Corleone crime family. Two decades have passed, and crime kingpin Michael Corleone, now divorced
            from his wife Kay has nearly succeeded in keeping his promise that his family would one day be completely legitimate.
        </p-accordionTab>
        <p-accordionTab header="Godfather IV" [disabled]="true">
            After a break of more than 15 years, director Francis Ford Coppola and writer Mario Puzo returned to the well for this third and final story of the fictional Corleone crime family. Two decades have passed, and crime kingpin Michael Corleone, now divorced
            from his wife Kay has nearly succeeded in keeping his promise that his family would one day be completely legitimate.
        </p-accordionTab>
    </p-accordion>
</div>
```

> Buka homepage.component.ts

```
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { UtilityService } from '../../services/utility.service';
@Component({
    templateUrl: './homepage.component.html'
})

export class HomepageComponent implements OnInit{
    private titlehomepage: String = 'Halaman HomePage';
    private indextab: number = -1;

constructor(private utility: UtilityService, private router: Router){
}
    ngOnInit(): void {
    this.utility.isLogged().then((result: boolean) => {
        if (!result) {
            this.router.navigate(['/login']);
        }
    });
}

onTabOpen(event): void {
    this.indextab = event.index;
}
}
```

* Jalankan pada browser

##  PathParams - _ngFor (Cara Membuat dan Akses Array)

> Pada folder model buat file `company.model.ts`
> Definisikan attribut array dengan kode di bawah

```
export interface Company {
    name: string,
    description: string
}
```

> Pada folder mock buat file `companies.moc.ts` 
> Definisikan data yang akan di tampilkan dalam array

```
import { Company } from "../model/company.model";

export const COMPANIES: Company[] = [{
            name: 'Carticol',
            description: 'Francis Ford Coppolas legendary continuation and sequel to his landmark 1972 film, ' +
            'The_Godfather parallels the young Vito Corleones rise with his son Michaels spiritual fall, ' +
            'deepening The_Godfathers depiction of the dark side of the American dream. ' +
            'In the early 1900s, the child Vito flees his Sicilian village for America after the local Mafia kills his family. ' +
            'Vito struggles to make a living, legally or illegally, for his wife and growing brood in Little Italy, ' +
            'killing the local Black Hand Fanucci after he demands his customary cut of the tyros business. '
        },
        {
            name: 'Damuni',
            description: 'Francis Ford Coppolas legendary continuation and sequel to his landmark 1972 film, ' +
            'The_Godfather parallels the young Vito Corleones rise with his son Michaels spiritual fall, ' +
            'deepening The_Godfathers depiction of the dark side of the American dream. ' +
            'In the early 1900s, the child Vito flees his Sicilian village for America after the local Mafia kills his family. ' +
            'Vito struggles to make a living, legally or illegally, for his wife and growing brood in Little Italy, ' +
            'killing the local Black Hand Fanucci after he demands his customary cut of the tyros business. '
        },
        {
            name: 'Golas',
            description: 'Francis Ford Coppolas legendary continuation and sequel to his landmark 1972 film, ' +
            'The_Godfather parallels the young Vito Corleones rise with his son Michaels spiritual fall, ' +
            'deepening The_Godfathers depiction of the dark side of the American dream. ' +
            'In the early 1900s, the child Vito flees his Sicilian village for America after the local Mafia kills his family. ' +
            'Vito struggles to make a living, legally or illegally, for his wife and growing brood in Little Italy, ' +
            'killing the local Black Hand Fanucci after he demands his customary cut of the tyros business. '
        },
        {
            name: 'Carticol',
            description: 'Francis Ford Coppolas legendary continuation and sequel to his landmark 1972 film, ' +
            'The_Godfather parallels the young Vito Corleones rise with his son Michaels spiritual fall, ' +
            'deepening The_Godfathers depiction of the dark side of the American dream. ' +
            'In the early 1900s, the child Vito flees his Sicilian village for America after the local Mafia kills his family. ' +
            'Vito struggles to make a living, legally or illegally, for his wife and growing brood in Little Italy, ' +
            'killing the local Black Hand Fanucci after he demands his customary cut of the tyros business. '
        }]
```

> Buka homepage.component.ts edit dan tambahkan kode di bawah

```
// Import Component
=======================================================
import { Company } from '../../model/company.model';
import { COMPANIES } from '../../mock/companies.mock';
=======================================================

// Di bawah class HomepageComponent
==============================
private companies: Company[];
==============================

dan

// Tambahkan pada ngOnInit()
============================
this.companies = COMPANIES;
============================
```

> Edit pada `homepage.component.html`

Perhatikan kode berikut untuk memanggil array menggunakan `*ngFor` :

```
` <p-accordionTab *ngFor="let item of companies" header="{{item.name}}">
            {{item.description}}
            <hr/> `
```

Kode Lengkap
```
<div class="main_content">
    <h1>List Didit</h1>
    <p-accordion (onOpen)="onTabOpen($event)">
        <p-accordionTab *ngFor="let item of companies" header="{{item.name}}">
            {{item.description}}
            <hr/>
            <button class="btn_accordian" pButton type="button" (click)="goToCalendar()" label="calendiaro"></button>
        </p-accordionTab>
    </p-accordion>
</div>
```

## Membuat Detail Component
> Membuat detail component calender, saat di klik akan muncul header.

Buat strukture file seperti : `\pages\details\calender_company.component.ts`
dan tambahkan kode seperti di bawah

```
import { Component, OnInit } from '@angular/core';
// Menambahkan import component
import { Subscription } from 'rxjs';
import { Router, ActivatedRoute } from '@angular/router';

@Component({
    templateUrl: './calender_company.component.html'
})

export class CalenderCompanyComponent implements OnInit{

    // Menambahkan subscription
    private calenderName: String;
    private subscription: Subscription;

    constructor(private activatedRouter: ActivatedRoute, private router: Router){
    }

    ngOnInit(): void {
        this.subscription = this.activatedRouter.params.subscribe(
            (param: any) => {
                this.calenderName = param['name'];
            }
        )
    }
}
```

Buat strukture file seperti : `\pages\details\calender_company.component.html`

```
// Template Menampilkan data pada calender_company.component.html
<h1>{{calenderName}}!!!</h1>
```

Pada `app.module.ts` tambahkan import module di bawah

```
// Menambahkan pages detail kedalam app.module.ts
import { CalenderCompanyComponent } from "./pages/details/calender_company.component";

@NgModule({
  declarations: [
    CalenderCompanyComponent
  ],
```

Pada `app.routes.ts` tambahkan path di bawah:

```
// Menambahkan path calender
    {
        path: 'calender/:name',
        component: CalenderCompanyComponent
    }

```

Pada `homepage.component.ts` tambahkan kode di bawah

```
// Fungsi menampilkan saat tombol calender di klik
public goToCalendar(): void {
    // alert("ini alert calender: " + this.indextab);
    this.router.navigate(['calender', this.companies[this.indextab].name]);
}
```

> Jalankan pada browser