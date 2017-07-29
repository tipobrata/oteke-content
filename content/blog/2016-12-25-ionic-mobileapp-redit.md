+++
title = "Ionic dan Web Service"
date = "2016-12-25T21:49:20+02:00"
tags = ["angular", "ionic"]
categories = ["Ionic"]
author = "diditwbw"
+++

## Membuat applikasi ionic dan menggunakan web service

 - $ ionic start ionreddit --v2
 - Buka http://localhost:8100/

Kita akan mengganti halaman `home` dan ` contact` menjadi `reddits` dan `settings`, kita akan mengambil contoh dari folder `about` berikut langkah nya.

Folder yang harus di pahami :

- `/ionreddit/src/app/app.module.ts`

- `/ionreddit/src/pages`

- `/ionreddit/src/pages/tabs`


## 1. Buka Folder `app` -> `/ionreddit/src/app/app.module.ts`

 ```
    import { NgModule, ErrorHandler } from '@angular/core';
    import { IonicApp, IonicModule, IonicErrorHandler } from 'ionic-angular';
    import { MyApp } from './app.component';
    import { AboutPage } from '../pages/about/about';
    import { RedditsPage } from '../pages/reddits/reddits';
    import { SettingsPage } from '../pages/settings/settings';
    import { TabsPage } from '../pages/tabs/tabs';

    @NgModule({
      declarations: [
        MyApp,
        AboutPage,
        RedditsPage,
        SettingsPage,
        TabsPage
      ],
      imports: [
        IonicModule.forRoot(MyApp)
      ],
      bootstrap: [IonicApp],
      entryComponents: [
        MyApp,
        AboutPage,
        RedditsPage,
        SettingsPage,

        TabsPage
      ],
      providers: [{provide: ErrorHandler, useClass: IonicErrorHandler}]
    })
    export class AppModule {}


 ```

## 2. Buka Folder `page` `/ionreddit/src/pages`

    
    Buat 2 Buat folder `reddits` dan `settings` copy file *.ts dan *.html ke dalam folder yang sudah di buat, dari folder `about`. edit file rubah sesuai nama.

## 3. Buka folder `tabs`

* isi file `tabs.ts`
   
        ```
            import { Component } from '@angular/core';

            import { RedditsPage } from '../reddits/reddits';
            import { AboutPage } from '../about/about';
            import { SettingsPage } from '../settings/settings';

            @Component({
              templateUrl: 'tabs.html'
            })
            export class TabsPage {
              // this tells the tabs component which Pages
              // should be each tab's root Page
              tab1Root: any = RedditsPage;
              tab2Root: any = SettingsPage;
              tab3Root: any = AboutPage;

              constructor() {

              }
            }
        ```

* file `tabs.html`

        ```
            <ion-tabs color="primary">
              <ion-tab [root]="tab1Root" tabTitle="Reddits" tabIcon="home"></ion-tab>
              <ion-jtab [root]="tab2Root" tabTitle="Settings" tabIcon="construct"></ion-tab>
              <ion-tab [root]="tab3Root" tabTitle="About" tabIcon="information-circle"></ion-tab>
            </ion-tabs>

        ```

## 4. Buat folder `services` -> `/ionreddit/src/app/services`

* Buat file -> `/ionreddit/src/app/services/reddit.service.ts`

        ```
            import { Injectable } from '@angular/core';
            import { Http } from '@angular/http';
            import 'rjx/Rx';

            @Injectable()
            export class RedditService{
                http:any;
                baseUrl: String;

                constructor(http:Http){
                    this.http = http;
                    this.baseUrl = 'https://www.reddit.com/r';
                }

                getPosts(category, limit){
                    return this.http.get(this.baseUrl+'/'+category+'/top.json?limit='+limit)
                        .map(res => res.json());
                }
            }

        ```
    
* Buka file `app.component.ts` Tambahkan / import, code di bawah letaknya di atas `import TabsPage`
    
    ```
        import { RedditService} from './services/reddit.service';
    ```

* Buka file `/ionreddit/src/pages/reddits/reddits.ts` tambahkan import di bawah
    
    ```
        import { RedditService} from '../../app/services/reddit.service';
    ```

    - Test menggunakan console.log
    ```
         ngOnInit(){
            console.log('onLine Init...');
          }
    ```

* Edit class `RedditPages` berada pada file `reddit.ts` menjadi seperti di bawah :
    
```
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import {RedditService} from '../../app/services/reddit.service';


@Component({
  selector: 'reddits',
  templateUrl: 'reddits.html'
})
export class RedditsPage {
  
  items:any;    
  constructor(public navCtrl: NavController, private redditService:RedditService) {

  }

  ngOnInit(){
    this.getPosts('sports', 10);
  }

  getPosts(category, limit){
    this.redditService.getPosts(category, limit).subscribe(response =>{
      //console.log(response);
      this.items = response.data.children;
    });
  }

}
```

* Edit `reddits.html` menjadi seperti di bawah : 

```
<ion-header>
    <ion-navbar color="primary">
        <ion-title>
            Reddits
        </ion-title>
    </ion-navbar>
</ion-header>

<ion-content padding>
    <ion-list>
        <ion-item *ngFor="let item of items">
            <ion-thumbnail *ngIf="item.data.thumbnail" item-left>
                <img src="{{item.data.thumbnail}}">
            </ion-thumbnail>
            <h2>{{item.data.title}}</h2>
            <p>
                <ion-icon name="thumbs-up">{{item.data.score}}</ion-icon>&nbsp;&nbsp;
                <ion-icon name="chatboxes">{{item.data.num_comments}}</ion-icon>
            </p>
            <button ion-button clear item-right (click)="viewItem()">View</button>
        </ion-item>
    </ion-list>
</ion-content>
```

* Menambahkan button click untuk melihat artikel dengan method `viewItem()`

```
<button ion-button clear item-right (click)="viewItem()">View</button>
```

* Agar method `viewItem()` berfungsi saat di klik, edit file `reddit.ts` dan tambahkan method di bawah :

```
viewItem(item){
    this.navCtrl.push(DetailsPage, {
      item: item
    })
  }
```

* Import pada file `reddit.ts` dan `app.module.ts` dan jangan lupa tambahkan `DetailsPage` juga pada `@NgModule`

```
import {DetailsPage} from '../details/details';
```

* Edit `details.ts` menjadi seperti di bawah :

```
import { Component } from '@angular/core';
import { NavController, NavParams } from 'ionic-angular';

@Component({
  templateUrl: 'details.html'
})
export class DetailsPage {
item: any;
  constructor(public navCtrl: NavController, public Params: NavParams ) {
        this.item = Params.get('item');
  }

}
```

* Edit `details.html` menjadi seperti di bawah :

```
<ion-header>
    <ion-navbar color="primary">
        <ion-title>
            {{item.title}}
        </ion-title>
    </ion-navbar>
</ion-header>
<ion-content padding>
    <ion-card>
        <img src="{{item.preview.images[0].source.url}}" />
        <ion-card-content>
            <ion-card-title>
                {{item.title}}
            </ion-card-title>
            <ion-list>
                <ion-item>
                    <ion-icon name="person" item-left></ion-icon>
                    Author
                    <ion-note item-right>
                        {{item.author}}
                    </ion-note>
                </ion-item>
                <ion-item>
                    <ion-icon name="thumbs-up" item-left></ion-icon>
                    Score
                    <ion-note item-right>
                        {{item.score}}
                    </ion-note>
                </ion-item>
                <ion-item>
                    <ion-icon name="chatsbox" item-left></ion-icon>
                    Comments
                    <ion-note item-right>
                        {{item.num_comments}}
                    </ion-note>
                </ion-item>
            </ion-list>
            <a ion-button block target="_blank" href="https://reddit.com/{{item.permalink}}">lihat di reddit</a>
        </ion-card-content>
    </ion-card>
</ion-content>
```

* Cara Membuat List Category, edit dan tambahkan kode di bawah pada `reddits.html` di bawah `<ion-content padding>`

```
<ion-list>
        <ion-item>
            <ion-label fixed>Category</ion-label>
            <ion-select (ionChange)="changeCategory()" [(ngModel)]="category" name="category">
                <ion-option value="sports">Sports</ion-option>
                <ion-option value="food">Food</ion-option>
                <ion-option value="news">News</ion-option>
                <ion-option value="music">Music</ion-option>
                <ion-option value="movie">Movie</ion-option>
                <ion-option value="funny">Funny</ion-option>
                <ion-option value="gaming">Gaming</ion-option>
                <ion-option value="internetisbeautiful">InternetIsBeautiful</ion-option>
                <ion-option value="realchinagirls">RealChinaGirl</ion-option>
                <ion-option value="art">Art</ion-option>
            </ion-select>
        </ion-item>
    </ion-list>

```

* Fungsi `changeCategory`, buka `reddit.ts`

* Method changeCategory

```
  changeCategory(){
    this.getPosts(this.category, this.limit);
  }
```

* Buat property Category

```
  category: any;
  limit: any; 
```

* Berikut kode lengkap nya `reddit.ts`

```
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import {RedditService} from '../../app/services/reddit.service';
import {DetailsPage} from '../details/details';

@Component({
  selector: 'reddits',
  templateUrl: 'reddits.html'
})
export class RedditsPage {  
  items:any;
  category: any;
  limit: any;   
  constructor(public navCtrl: NavController, private redditService:RedditService) {
    this.getDefaults();
 }

  ngOnInit(){
    this.getPosts(this.category, this.limit);
  }

  getDefaults(){
    this.category = "sports";
    this.limit = "10";
  }

  getPosts(category, limit){
    this.redditService.getPosts(category, limit).subscribe(response =>{
      //console.log(response);
      this.items = response.data.children;
    });
  }

  viewItem(item){
    this.navCtrl.push(DetailsPage, {
      item: item
    })
  }

  changeCategory(){
    this.getPosts(this.category, this.limit);
  }

}
```

#Tabs Settings

* edit settings.ts menjadi seperti di bawah :

```
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import {RedditService} from '../../app/services/reddit.service';

@Component({
  selector: 'settings',
  templateUrl: 'settings.html'
})
export class SettingsPage {
  category: any;
  limit: any;   
  constructor(public navCtrl: NavController, private redditService:RedditService) {
    this.getDefaults();
 }

  getDefaults(){
    this.category = "sports";
    this.limit = "10";
  }

}
```

* edit settings.html

```
<ion-header>
    <ion-navbar color="primary">
        <ion-title>
            Settings
        </ion-title>
    </ion-navbar>
</ion-header>

<ion-content padding>
    <form (submit)="setDefault()">
        <ion-list>
            <ion-item>
                <ion-label fixed>Category</ion-label>
                <ion-select [(ngModel)]="category" name="category">
                    <ion-option value="sports">Sports</ion-option>
                    <ion-option value="food">Food</ion-option>
                    <ion-option value="news">News</ion-option>
                    <ion-option value="music">Music</ion-option>
                    <ion-option value="movie">Movie</ion-option>
                    <ion-option value="funny">Funny</ion-option>
                    <ion-option value="gaming">Gaming</ion-option>
                    <ion-option value="internetisbeautiful">InternetIsBeautiful</ion-option>
                    <ion-option value="realchinagirls">RealChinaGirl</ion-option>
                    <ion-option value="art">Art</ion-option>
                </ion-select>
            </ion-item>
            <ion-item>
                <ion-label fixed>Limit</ion-label>
                <ion-select [(ngModel)]="limit" name="limit">
                    <ion-option value="5">5</ion-option>
                    <ion-option value="10">10</ion-option>
                    <ion-option value="15">15</ion-option>
                    <ion-option value="20">20</ion-option>
                    <ion-option value="25">25</ion-option>
                </ion-select>
            </ion-item>
            <button ion-button type="submit" block>Save Change</button>
        </ion-list>
    </form>
</ion-content>
```

> local Storage untuk simpan data sementara tambahkan method `setDefault()` dan edit `getDefault()`

```
  getDefaults(){
    if(localStorage.getItem('category') != null){
      this.category = localStorage.getItem('category')
    }else{
      this.category = 'sports';
    }
    if(localStorage.getItem('limit') != null){
      this.category = localStorage.getItem('limit')
    }else{
      this.category = 10;
    }
  }
  setDefault(){
    localStorage.setItem('category', this.category);
    localStorage.setItem('limit', this.limit);
    this.navCtrl.push(RedditsPage);
  }
```

* pada `reddit.ts` edit method `getDefault()`

```
  getDefaults(){
    if(localStorage.getItem('category') != null){
      this.category = localStorage.getItem('category')
    }else{
      this.category = 'sports';
    }
    if(localStorage.getItem('limit') != null){
      this.category = localStorage.getItem('limit')
    }else{
      this.category = 10;
    }
  }
```

# Build Applikasi Android

```
    $ cordova platform add android
    $ npm info cordova version // melihat versi cordova
```


# Build APK

```
$ cordova platform add android

//menjalankan ionic di emulator
$ ionic run android

// membuild program menjadi apk
$ ionic build android
```



# Error Problem
Error
Error:Unable to start the daemon process.
This problem might be caused by incorrect configuration of the daemon.
For example, an unrecognized jvm option is used.
Please refer to the user guide chapter on the daemon at https://docs.gradle.org/2.14.1/userguide/gradle_daemon.html
Please read the following process output to find out more:

Error occurred during initialization of VM
Could not reserve enough space for 1572864KB object heap

# Solution
This means the JVM hasn't enough memory space. Adding following property in the gradle.properties file will fix your problem:
1.Open the projects gradle.properties file in android studio
2.Added this line at end of file `org.gradle.jvmargs=-Xmx1024m` & Save the file
3.Close & reopen the project