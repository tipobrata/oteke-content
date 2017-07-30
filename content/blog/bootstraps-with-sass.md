+++
title = "Bootstraps dengan Sass"
date = "2017-04-30T21:49:20+02:00"
tags = ["sass", "bootstraps"]
categories = ["frontend"]
author = "tipobrata"
+++

## Install Bower dari npm

```
D:\Tools\Tutorial-Template\mythemes>npm install -g bower
C:\Users\My PC\AppData\Roaming\npm\bower -> C:\Users\My PC\AppData\Roaming\npm\node_modules\bower\bin\bower
C:\Users\My PC\AppData\Roaming\npm
`-- bower@1.8.0
```

## Install bootstrap-sass ke dalam folder project

```
$ bower install bootstrap-sass --save

D:\Tools\Tutorial-Template\mythemes>bower install bootstrap-sass --save
bower bootstrap-sass#*          cached https://github.com/twbs/bootstrap-sass.git#3.3.7
bower bootstrap-sass#*        validate 3.3.7 against https://github.com/twbs/bootstrap-sass.git#*
bower jquery#1.9.1 - 3          cached https://github.com/jquery/jquery-dist.git#3.2.1
bower jquery#1.9.1 - 3        validate 3.2.1 against https://github.com/jquery/jquery-dist.git#1.9.1 - 3
bower bootstrap-sass#^3.3.7    install bootstrap-sass#3.3.7
bower jquery#1.9.1 - 3         install jquery#3.2.1
bower                          no-json No bower.json file to save to, use bower init to create one

bootstrap-sass#3.3.7 bower_components\bootstrap-sass
└── jquery#3.2.1

jquery#3.2.1 bower_components\jquery
```

Buat folder `sass` dan `stylesheets` dalam folder project, buat file dengan nama `app.scss` di dalam folder `sass` dan import bootsrap-sass dengan cara ketikkan kpode di bawah:

```
@import "../bower_components/bootstrap-sass/assets/stylesheets/bootstrap";
@import "../bower_components/bootstrap-sass/assets/stylesheets/bootstrap-compass";
```

> Buka applikasi `koala` tambahkan folder `sass` ke dalam applikasi koala dan akan terbentuk folder `css` dan dua buah file `app.css` dan `app.css.map`

> Buat file `index.html` 

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My Themes</title>
    <link rel="stylesheet" href="css/app.css">
  </head>

  <body>

    <nav class="navbar navbar-default">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">Project name</a>
        </div>
        <div id="navbar" class="collapse navbar-collapse">
          <ul class="nav navbar-nav">
            <li class="active"><a href="#">Home</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </div><!--/.nav-collapse -->
      </div>
    </nav>

    <div class="container">

      <div class="starter-template">
        <h1>Bootstrap starter template</h1>
        <p class="lead">Use this document as a way to quickly start any new project.<br> All you get is this text and a mostly barebones HTML document.</p>
      </div>

    </div><!-- /.container -->


    </body>
</html>
```

Install live-server dalam folder project

```
npm install -g live-server
```

kemudian jalankan perintah `live-server` dalam folder project, dan akan muncul pada web browser dengan port `http://127.0.0.1:8080/`

## Menggunakan Variabel Bootstraps
Untuk bisa menggunakan variabel bootstrap, langkah yang di lakukan adalah:

**1. copy isi file `_variables.scss` (lihat path di bawah).**

```
\mythemes\bower_components\bootstrap-sass\assets\stylesheets\bootstrap\_variables.scss
```

**2. paste ke dalam file `_customVariabel.scss` (jika belum ada buat terlebih dahulu).**

```
\mythemes\sass\_customVariabel.scss
```

**3. dan import ke dalam file `app.scss`**

```
@import "customVariables";
```

**4. Merubah warna atau menetapkan main-warna pada `navbar`, buka file `_customVariabel.scss`, dan tambahkan kode di bawah:**

**Memilih Warna:** 
A. [kulay.org](http://kulay.org)

B. [Hexdictionary](https://www.hexdictionary.com)

```
// custom main
$main-color: #1a8c97;
```

**cari baris `375` atau rubah menjadi seperti di bawah:**

```
// Basics of a navbar
$navbar-default-bg:                $main-color !default;

// Navbar links
$navbar-default-link-color:                #fff !default;
$navbar-default-link-hover-color:          #fff !default;
$navbar-default-link-active-color:         #fff !default;
```

**Pada Baris di bawah rubah menjadi seperti ini:**

```
$navbar-default-link-hover-bg:             darken($navbar-default-bg, 6.5%) !default;
$navbar-default-link-active-color:         #fff !default;
$navbar-default-link-active-bg:            darken($navbar-default-bg, 6.5%) !default;
```

## Install FontAwesome

**install fontawesome ke dalam project**

```
bower install fontawesome --save
```

> Cara penggunaannya:

**1. Import kedalam file `app.scss`**

```
@import "../bower_components/font-awesome/scss/font-awesome";
```

**2. copy folder `font` yang ada dalam folder `font-awesome` ke dalam folder root project.**

```
/bower_components/fonts
```

**4. Buka file `index.html`, tambah kan `navbar-right`**

```
<ul class="nav navbar-nav navbar-right">
            <li><a href="http://twitter.com"><i class="fa fa-twitter"></i></a></li>
            <li><a href="http://facebook.com"><i class="fa fa-facebook"></i></a></li>
            <li><a href="http://google-plus.com"><i class="fa fa-google-plus"></i></a></li>
            <li><a href="http://linkedin.com"><i class="fa fa-linkedin"></i></a></li>
</ul>
```

**5. Buat `cutom.scss` untuk custom navbar, isi dengan kode di bawah dan jangan lupa untuk import pada file `app.scss`:**

```
.navbar {
    .fa{
        font-size:18px;
    }
}
```

## Container

A. [Lipsum](http://www.lipsum.com/)

B. [Free Foto](https://www.pexels.com/)

**1. Buka file `index.html`**
Tambahkan kode di bawah di dalam tag body di bawah nav:

```
    <div class="showcase">
      <div class="container">
          <h1>Dapatkan???</h1>
          <p class="lead">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."</p>
          <a href="about.html" class="btn btn-primary">Read More</a>
      </div><!-- /.container -->
    </div>

    <div class="section-a">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <i class="fa fa-html5"></i>
            <h3>Clean and Simple Code</h3>
            <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."</p>
          </div>
          <div class="col-md-4">
            <i class="fa fa-gear"></i>
            <h3>Clean and Simple Code</h3>
            <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."</p>
          </div>
          <div class="col-md-4">
            <i class="fa fa-lightbulb-o"></i>
            <h3>Clean and Simple Code</h3>
            <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."</p>
          </div>
          
        </div>
      </div>
    </div>
```

**2. Buka file custom.scss dan tambahkan kode di bawah**

```
.navbar {
    margin-bottom:0;
    a{
        color: set-text-color($main-color) !important;
    }
    .fa{
        font-size:18px;
    }
}

.showcase{
    background: url(../images/pexels-photo.jpeg) no-repeat 0 -100px;
    height: 400px;
    padding: 30px 0;

    h1{
        font-size: 60px;
    }
    .container{
        background: #fff;
        opacity: 0.8;
        padding: 20px 30px 30px 30px;
    }
}

.section-a{
    padding: 30px 0;
    text-align: center;
    background: $main-color;
    color: set-text-color($main-color);

    .fa{
        font-size: $icon-size;
    }
}
```

**3. Buat file `_function.scss` isi dengan code di bawah(Jangan lupa import pada file app.scss):**

```
@function set-text-color($color) {
    @if (lightness($color) > 50){
        @return #000000;        
    } @else {
        @return #ffffff;
    }
}
```

**4. Insert file javascript**
```
    <script src="bower_components/jquery/dist/jquery.js"></script>
    <script src="bower_components/bootstrap-sass/assets/javascripts/bootstrap.js"></script>
```

**5. Menambahkan panel Heading dan Gambar**

`index.html`

```
<div class="section-b">
      <div class="container">
        <div class="row">
          <div class="col-md-6">
            <div class="panel-group" id="accordion" role="tablist" aria-multiselectable="true">
  <div class="panel panel-default">
    <div class="panel-heading" role="tab" id="headingOne">
      <h4 class="panel-title">
        <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
          Collapsible Group Item #1
        </a>
      </h4>
    </div>
    <div id="collapseOne" class="panel-collapse collapse in" role="tabpanel" aria-labelledby="headingOne">
      <div class="panel-body">
        Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
      </div>
    </div>
  </div>
  <div class="panel panel-default">
    <div class="panel-heading" role="tab" id="headingTwo">
      <h4 class="panel-title">
        <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
          Collapsible Group Item #2
        </a>
      </h4>
    </div>
    <div id="collapseTwo" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingTwo">
      <div class="panel-body">
        Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
      </div>
    </div>
  </div>
  <div class="panel panel-default">
    <div class="panel-heading" role="tab" id="headingThree">
      <h4 class="panel-title">
        <a class="collapsed" role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseThree" aria-expanded="false" aria-controls="collapseThree">
          Collapsible Group Item #3
        </a>
      </h4>
    </div>
    <div id="collapseThree" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingThree">
      <div class="panel-body">
        Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
      </div>
    </div>
  </div>
</div>
          </div>
          <div class="col-md-6">
            <img src="images/cpu.jpeg">
          </div>      
        </div>
      </div>
    </div>
```

`Custom.scss`

```
.section-b{
    background:#e6ebf1;
    padding: 30px 0;

    img{
        width: 100%;
    }
}

.panel-heading h4{
    color: set-text-color($main-color);
}
```


**untuk merubah warna panel-heading cari baris di bawah pada `customVariables.scss`**

```
$panel-default-heading-bg:    $main-color !default;
```

**6. Subcribe dan Footer**

```
<div class="section-c">
      <div class="container">
        <div class="row">
          <div class="col-md-8 col-md-offset-2">
              <h2>Subcribe Our News latters</h2>
              <br/>
              <form>
                <input type="text" class="form-control input-lg" placeholder="Enter Email">
                <br/>
                <button class="btn btn-primary btn-lg btn-block">Submit</button>
              </form>
          </div>
        </div>
      </div>
    </div>

    <footer>
        <div class="container">
            <p>Copyright &copy; 2017 MyTheme</p>
        </div>
    </footer>
```

**`Custom.scss`**

```
.section-c{
    padding: 60px 0;
    text-align: center;
    background: $main-color;
    color: set-text-color($main-color);

    .btn-primary{
        background: darken($main-color, 10%);
    }
}

.title-bar{
    background: url(../images/pexels-photo.jpeg) no-repeat 0 -300px;
    padding-bottom: 10px;
    border-bottom: 4px solid $main-color;
    color: set-text-color($main-color);
}

.main{
    margin-top: 30px;
}

footer{
    padding: 30px 0;
    text-align: center;
    background: darken($main-color, 10%);
    color: set-text-color($main-color);
}
```

## Page About

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My Themes | About</title>
    <link rel="stylesheet" href="css/app.css">
  </head>

  <body>

    <nav class="navbar navbar-default">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">My Themes</a>
        </div>
        <div id="navbar" class="collapse navbar-collapse">
          <ul class="nav navbar-nav">
            <li><a href="index.html">Home</a></li>
            <li class="active"><a href="about.html">About</a></li>
            <li><a href="services.html">Services</a></li>
            <li><a href="contact.html">Contact</a></li>
          </ul>
          <ul class="nav navbar-nav navbar-right">
            <li><a href="http://twitter.com"><i class="fa fa-twitter"></i></a></li>
            <li><a href="http://facebook.com"><i class="fa fa-facebook"></i></a></li>
            <li><a href="http://google-plus.com"><i class="fa fa-google-plus"></i></a></li>
            <li><a href="http://linkedin.com"><i class="fa fa-linkedin"></i></a></li>
          </ul>
        </div><!--/.nav-collapse -->
      </div>
    </nav>

    <div class="title-bar">
      <div class="container">
          <h1>About</h1>
          
      </div><!-- /.container -->
    </div>

    <div class="main">
    <div class="container">
      <div class="row">
        <div class="col-md-8">
            <div class="panel panel-default">
              <div class="panel-heading">
                <h4 class="panel-title">Tentang Kita</h4>
              </div>
              <div class="panel-body">
                <p>"Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur? Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae consequatur, vel illum qui dolorem eum fugiat quo voluptas nulla pariatur?"</p>
              </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="list-group">
              <a href="#" class="list-group-item active">
               Cras justo odio</a>
              <a href="#" class="list-group-item">Dapibus ac facilisis in</a>
              <a href="#" class="list-group-item">Morbi leo risus</a>
              <a href="#" class="list-group-item">Porta ac consectetur ac</a>
              <a href="#" class="list-group-item">Vestibulum at eros</a>
            </div>
        </div>
      </div>
    </div>
    </div>

    <div class="section-c">
      <div class="container">
        <div class="row">
          <div class="col-md-8 col-md-offset-2">
              <h2>Subcribe Our News latters</h2>
              <br/>
              <form>
                <input type="text" class="form-control input-lg" placeholder="Enter Email">
                <br/>
                <button class="btn btn-primary btn-lg btn-block">Submit</button>
              </form>
          </div>
        </div>
      </div>
    </div>

    <footer>
        <div class="container">
            <p>Copyright &copy; 2017 MyTheme</p>
        </div>
    </footer>
    <script src="bower_components/jquery/dist/jquery.js"></script>
    <script src="bower_components/bootstrap-sass/assets/javascripts/bootstrap.js"></script>
    </body>
</html>

```

## Page Services

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My Themes | Services</title>
    <link rel="stylesheet" href="css/app.css">
  </head>

  <body>

    <nav class="navbar navbar-default">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">My Themes</a>
        </div>
        <div id="navbar" class="collapse navbar-collapse">
          <ul class="nav navbar-nav">
            <li><a href="index.html">Home</a></li>
            <li><a href="about.html">About</a></li>
            <li class="active"><a href="services.html">Services</a></li>
            <li><a href="contact.html">Contact</a></li>
          </ul>
          <ul class="nav navbar-nav navbar-right">
            <li><a href="http://twitter.com"><i class="fa fa-twitter"></i></a></li>
            <li><a href="http://facebook.com"><i class="fa fa-facebook"></i></a></li>
            <li><a href="http://google-plus.com"><i class="fa fa-google-plus"></i></a></li>
            <li><a href="http://linkedin.com"><i class="fa fa-linkedin"></i></a></li>
          </ul>
        </div><!--/.nav-collapse -->
      </div>
    </nav>

    <div class="title-bar">
      <div class="container">
          <h1>Services</h1>
          
      </div><!-- /.container -->
    </div>

    <div class="main">
    <div class="container">
      <div class="row">
        <div class="col-md-8">
            <div class="panel panel-default">
              <div class="panel-heading">
                <h4 class="panel-title">For You</h4>
              </div>
              <div class="panel-body">
                <div class="well">
                  <h4>Web Design Grafish</h4>
                  <p>Lorem Ipsum adalah text contoh digunakan didalam industri pencetakan dan typesetting. Lorem Ipsum telah menjadi text contoh semenjak tahun ke 1500an, apabila pencetak yang kurang terkenal mengambil sebuah galeri cetak dan merobakanya menjadi satu buku spesimen. Ia telah bertahan bukan hanya selama lima kurun, tetapi telah melonjak ke era typesetting elektronik, dengan tiada perubahan ketara. Ia telah dipopularkan pada tahun 1960an dengan penerbitan Letraset yang mebawa kangungan Lorem Ipsum, dan lebih terkini dengan sofwer pencetakan desktop seperti Aldus PageMaker yang telah menyertakan satu versi Lorem Ipsum.</p>
                </div>
                <div class="well">
                  <h4>Service Komputer</h4>
                  <p>Lorem Ipsum adalah text contoh digunakan didalam industri pencetakan dan typesetting. Lorem Ipsum telah menjadi text contoh semenjak tahun ke 1500an, apabila pencetak yang kurang terkenal mengambil sebuah galeri cetak dan merobakanya menjadi satu buku spesimen. Ia telah bertahan bukan hanya selama lima kurun, tetapi telah melonjak ke era typesetting elektronik, dengan tiada perubahan ketara. Ia telah dipopularkan pada tahun 1960an dengan penerbitan Letraset yang mebawa kangungan Lorem Ipsum, dan lebih terkini dengan sofwer pencetakan desktop seperti Aldus PageMaker yang telah menyertakan satu versi Lorem Ipsum.</p>
                </div>
                <div class="well">
                  <h4>Web Developer</h4>
                  <p>Lorem Ipsum adalah text contoh digunakan didalam industri pencetakan dan typesetting. Lorem Ipsum telah menjadi text contoh semenjak tahun ke 1500an, apabila pencetak yang kurang terkenal mengambil sebuah galeri cetak dan merobakanya menjadi satu buku spesimen. Ia telah bertahan bukan hanya selama lima kurun, tetapi telah melonjak ke era typesetting elektronik, dengan tiada perubahan ketara. Ia telah dipopularkan pada tahun 1960an dengan penerbitan Letraset yang mebawa kangungan Lorem Ipsum, dan lebih terkini dengan sofwer pencetakan desktop seperti Aldus PageMaker yang telah menyertakan satu versi Lorem Ipsum.</p>
                </div>
              </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="list-group">
              <a href="#" class="list-group-item active">
               Cras justo odio</a>
              <a href="#" class="list-group-item">Dapibus ac facilisis in</a>
              <a href="#" class="list-group-item">Morbi leo risus</a>
              <a href="#" class="list-group-item">Porta ac consectetur ac</a>
              <a href="#" class="list-group-item">Vestibulum at eros</a>
            </div>
        </div>
      </div>
    </div>
    </div>

    <div class="section-c">
      <div class="container">
        <div class="row">
          <div class="col-md-8 col-md-offset-2">
              <h2>Subcribe Our News latters</h2>
              <br/>
              <form>
                <input type="text" class="form-control input-lg" placeholder="Enter Email">
                <br/>
                <button class="btn btn-primary btn-lg btn-block">Submit</button>
              </form>
          </div>
        </div>
      </div>
    </div>

    <footer>
        <div class="container">
            <p>Copyright &copy; 2017 MyTheme</p>
        </div>
    </footer>
    <script src="bower_components/jquery/dist/jquery.js"></script>
    <script src="bower_components/bootstrap-sass/assets/javascripts/bootstrap.js"></script>
    </body>
</html>

```

## Page Contact

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My Themes | Contact</title>
    <link rel="stylesheet" href="css/app.css">
  </head>

  <body>

    <nav class="navbar navbar-default">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">My Themes</a>
        </div>
        <div id="navbar" class="collapse navbar-collapse">
          <ul class="nav navbar-nav">
            <li><a href="index.html">Home</a></li>
            <li><a href="about.html">About</a></li>
            <li><a href="services.html">Services</a></li>
            <li class="active"><a href="contact.html">Contact</a></li>
          </ul>
          <ul class="nav navbar-nav navbar-right">
            <li><a href="http://twitter.com"><i class="fa fa-twitter"></i></a></li>
            <li><a href="http://facebook.com"><i class="fa fa-facebook"></i></a></li>
            <li><a href="http://google-plus.com"><i class="fa fa-google-plus"></i></a></li>
            <li><a href="http://linkedin.com"><i class="fa fa-linkedin"></i></a></li>
          </ul>
        </div><!--/.nav-collapse -->
      </div>
    </nav>

    <div class="title-bar">
      <div class="container">
          <h1>Contact</h1>
          
      </div><!-- /.container -->
    </div>

    <div class="main">
    <div class="container">
      <div class="row">
        <div class="col-md-8">
            <div class="panel panel-default">
              <div class="panel-heading">
                <h4 class="panel-title">Sentuh dan Dapatkan</h4>
              </div>
              <div class="panel-body">
                <form>
                    <div class="form-group">
                      <label>Nama</label>
                      <input type="text" class="form-control" placeholder="Nama">
                    </div>
                    <div class="form-group">
                      <label>Nama</label>
                      <input type="email" class="form-control" placeholder="Email">
                    </div>
                    <div class="form-group">
                      <label>Messages</label>
                      <textarea type="text" class="form-control" placeholder="Messages"></textarea>
                    </div>
                    <button type="Submit" class="btn btn-default">Submit</button>
                </form>
              </div>
            </div>
        </div>
        <div class="col-md-4">
            <div class="list-group">
              <a href="#" class="list-group-item active">
               Cras justo odio</a>
              <a href="#" class="list-group-item">Dapibus ac facilisis in</a>
              <a href="#" class="list-group-item">Morbi leo risus</a>
              <a href="#" class="list-group-item">Porta ac consectetur ac</a>
              <a href="#" class="list-group-item">Vestibulum at eros</a>
            </div>
        </div>
      </div>
    </div>
    </div>

    <div class="section-c">
      <div class="container">
        <div class="row">
          <div class="col-md-8 col-md-offset-2">
              <h2>Subcribe Our News latters</h2>
              <br/>
              <form>
                <input type="text" class="form-control input-lg" placeholder="Enter Email">
                <br/>
                <button class="btn btn-primary btn-lg btn-block">Submit</button>
              </form>
          </div>
        </div>
      </div>
    </div>

    <footer>
        <div class="container">
            <p>Copyright &copy; 2017 MyTheme</p>
        </div>
    </footer>
    <script src="bower_components/jquery/dist/jquery.js"></script>
    <script src="bower_components/bootstrap-sass/assets/javascripts/bootstrap.js"></script>
    </body>
</html>

```