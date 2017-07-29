+++
title = "Dasar Angular"
date = "2017-01-24T21:49:20+02:00"
tags = ["angular"]
categories = ["Angular"]
author = "diditwbw"
+++

## Belajar dasar angular
Sebelumnya download dan install [nodeJs](https://nodejs.org/en/) sesuai Os dan platform yang di gunakan, berikut cara Update npm secara global

```
npm install npm -g
```
**install npm secara global**

```
npm install npm -g 
```
**install angular-cli secara global**

```
npm install -g angular-cli
```
**install typescript secara global**

```
npm Install -g typescript 
```

**Memulai angular quickstart**

- download angular quickstar `https://github.com/angular/quickstart`
- extract, rename dan masuk folder untuk project angular sebagai contoh : `cd angular-start`
- jalankan `$ npm install` untuk install dependency yang di butuhkan, terletak di file `package.json`

- untuk menjalankan angular applikasi dengan perintah

    ```
    $ npm install
    $ npm start
    ```
- cek di layar browser `http://localhost:3000/`

**Contoh @component**

- Bagaimana Hello Angular bisa tampil pada web Browser, 
  see : `/Angular/myapp/angular-start/app/app.component.ts`

```
        import { Component } from '@angular/core';

        @Component({
          selector: 'my-app',
          template: `<h1>Hello {{name}}</h1>`,
        })
        export class AppComponent  { name = 'Didit'; }
```
    - membuat @component dengan nama `my-app` dan akan di tampilakn pada `index.html`

`/Angular/myapp/angular-start/index.html`

```
        </head>
          <body>

            //menampilkan @component `my-app` dari file `app.component.ts`
            <my-app>Loading AppComponent content here ...</my-app> 
            
          </body>
        </html>
```

**Menambah @Component**

- Buat Folder `/Angular/myapp/angular-start/app/components`
- Buat File `user.component.ts` di dalam folder `components`
- Dalam folder components akan terbentuk secara otomatis 2 file `user.component.js` dan `user.component.js.map`
- Sehingga dalam folder componenst terdapat 3 file yaitu :

    - `user.component.ts`
    - `file user.component.js`
    - `user.component.js.map`

- Edit `app.module.ts`, untuk mendaftarkan component yang kita buat, import / sisipkan kode berikut, di bawah import `AppComponent`

```
import { UserComponent }  from './components/user.component';
```

- Pada baris `@NgModule` baris `declarations` tambahkan `UserComponent` seperti kode di bawah 

```
declarations: [ AppComponent, UserComponent ],
```

- Edit `app.component.ts`, Untuk menampilkan isi dari `UserComponent` di dalam `AppComponent`, tambahkan kode menjadi seperti di bawah : 

- `<user></user>` -> merupakan data `UserComponent.ts` cek pada baris `selector: user`.

```
            import { Component } from '@angular/core';

            @Component({
              selector: 'my-app',
              template: `
                <user></user>
              `,
            })
            export class AppComponent  { 
                
            }
```

**Detail user.component.ts CRUD** 

```
    import {Component} from '@angular/core';

    @Component({
      selector: 'user',
      template: `
      <h1>{{name}}</h1>
      <p><strong>Email</strong> : {{email}}</p>
      <p><strong>Alamat :</strong> {{alamat.jalan}}, {{alamat.kota}}, {{alamat.provinsi}}.</p>
        <button (click)="toggleHobbies()">{{showHobbies ? "Hide Hobbies" : "Show Hobbies"}} 
          <h3>Hobbies</h3>
              <ul>
                <li *ngFor="let hobby of hobbies; let i = index">
                    {{hobby}} <button (click)="hapusHobi(i)">X</button>
                </li>
          </ul>
          <form (submit)="tambahHobi(hobby.value)">
            <label>Tambah Hobi : </label><br />
            <input type="text" #hobby /><br />
          </form>
      </div>
      <hr />
      <form>
            <label>Nama : </label><br />
            <input type="text" name="name" [(ngModel)]='name' /><br />
             <label>Email : </label><br />
            <input type="text" name="email" [(ngModel)]='email' /><br />
             <label>Alamat : </label><br />
            <input type="text" name="alamat.jalan" [(ngModel)]='alamat.jalan' /><br />
             <label>Kota : </label><br />
            <input type="text" name="alamat.kota" [(ngModel)]='alamat.kota' /><br />
             <label>Provinsi : </label><br />
            <input type="text" name="alamat.provinsi" [(ngModel)]='alamat.provinsi' /><br />
      </form>
      `,
    })
    export class UserComponent  { 
        name: string;
        email: string;
        alamat: alamat;
        hobbies: string[];
        showHobbies: boolean;

        constructor(){
            //console.log('constructor run');
        this.name = 'TipoBrata';
        this.email = 'tipobrata@gmail.com',
        this.alamat = {
            jalan: 'Jl. orogensi No. 000',
            kota: 'Semarang',
            provinsi: 'Jawa Tengah'
            }
        this.hobbies = ['Musik', 'Berenang', 'Menari dan', 'Shoping - Shoping'];
        this.showHobbies= false;
        }

        toggleHobbies(){
            if(this.showHobbies == true){
                this.showHobbies=false;
            } else {
                this.showHobbies=true;
                }
            }
        tambahHobi(hobby:any){
            this.hobbies.push(hobby);
        }

        hapusHobi(i:any){
            this.hobbies.splice(i,1);
        }
    }

    interface alamat {
        jalan: string;
        kota: string;
        provinsi: string;
    }

```

**Mengambil Data Postingan melalui webservice suatu web**

- Buat folder `services` letak path `/angular-start/app/services`
- Buat file `post.service.ts` di dalam folder `services` ketikkan kode di bawah.

```
        import { Injectable } from '@angular/core';
        import { Http } from '@angular/http';
        import 'rxjs/add/operator/map';

        @Injectable()
        export class PostsService{
            constructor(private http: Http){
                console.log('Initialize Ok');
            }

            getPosts(){
                return this.http.get('https://jsonplaceholder.typicode.com/posts')
                    .map(res => res.json());
            }
        }
```

- Pada file `user.component.ts` , tambahkan kode di bawah.
- Import class `PostsService` pada `user.component.ts`, copy code di bawah

```
import {PostsService} from '../services/post.service';
```
- Tambahkan kode di bawah, yang letaknya di bawah template.

```
        template: `

        `,
        providers: [PostsService]
```
- Pada Contructor, tambahkan kode di bawah.

```
        constructor(private postsService: PostsService){

        this.postsService.getPosts().subscribe(posts => {
            this.posts = posts;
            })
        }
```
- Pada class `user.component.ts`, tambahkan.

```
        posts: Post[];
```

- Tambahkan `interface` di bawah.

```
        interface Post{
            id: number;
            title: string;
            body: string;
        }
```
- pada file `html` tambahkan kode di bawah untuk menampilkan `post`

```
        <h3>Posts</h3>
          <div *ngFor="let post of posts">
                <h3>{{post.title}}</h3>
                <p>{{post.body}}</p>
          </div>
```

- Jalankan pada web server apakah muncul postingan dari `https://jsonplaceholder.typicode.com/posts'`

```
http://localhost:3000/
```

- edit `app.module.ts` menjadi seperti di bawah :

```
        import { NgModule }      from '@angular/core';
        import { BrowserModule } from '@angular/platform-browser';
        import { FormsModule } from '@angular/forms';
        import { HttpModule } from '@angular/http';


        import { AppComponent }  from './app.component';
        import { UserComponent }  from './components/user.component';

        @NgModule({
          imports:      [ BrowserModule, FormsModule, HttpModule ],
          declarations: [ AppComponent, UserComponent ],
          bootstrap:    [ AppComponent ]
        })
        export class AppModule { }
```

**Routing**

- Buat Folder `services` dan file `D:\Angular\angular-start\app\services\post-.service.ts` yang isinya :

```
        import { Injectable } from '@angular/core';
        import { Http } from '@angular/http';
        import 'rxjs/add/operator/map';

        @Injectable()
        export class PostsService{
            constructor(private http: Http){
                console.log('Initialize Ok');
            }

            getPosts(){
                return this.http.get('https://jsonplaceholder.typicode.com/posts')
                    .map(res => res.json());
            }
        }
```

- Buat file `app.routing.ts` lokasi `D:\Angular\angular-start\app\app.routing.ts` ketikkan kode di bawah :

```
    import {ModuleWithProviders} from '@angular/core';
    import {Routes, RouterModule} from '@angular/router';

    import {UserComponent} from './components/user.component';
    import {AboutComponent} from './components/about.component';

    const appRoutes: Routes = [
        {
            path:'',
            component: UserComponent
        },
        {
            path:'about',
            component: AboutComponent
        }
    ];

    export const routing: ModuleWithProviders = RouterModule.forRoot(appRoutes);
```

- Edit `app.modul.ts` tambahkan import di bawah :

```
    import { NgModule }      from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { FormsModule } from '@angular/forms';
    import { HttpModule } from '@angular/http';


    import { AppComponent }  from './app.component';
    import { UserComponent }  from './components/user.component';
    import { AboutComponent }  from './components/about.component';
    import {routing} from './app.routing';


    @NgModule({
      imports:      [ BrowserModule, FormsModule, HttpModule, routing ],
      declarations: [ AppComponent, UserComponent, AboutComponent ],
      bootstrap:    [ AppComponent ]
    })
    export class AppModule { }
```

- Edit `index.html` tambahkan kode, di bawah `<body>` :

```
    <body>
    <base href="/">
    <my-app>Loading AppComponent content here ...</my-app>
    </body>
```

- Edit `app.component.ts` menjadi seperti di bawah :

```
    import { Component } from '@angular/core';

    @Component({
      selector: 'my-app',
      template: `
        <ul>
            <li><a routerLink="/">Home</a></li>
            <li><a routerLink="about">About</a></li>
        </ul>

        <router-outlet><router-outlet>
      `,
    })
    export class AppComponent  { 
        
    }

```

- Buka browser `http://localhost:3000/` untuk melihat hasil nya.

nodejs: [node-js](https://nodejs.org/en/)