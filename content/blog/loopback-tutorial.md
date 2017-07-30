+++
title = "Loopback Framework"
date = "2017-05-21T21:49:20+02:00"
tags = ["strongloop", "loopback"]
categories = ["loopback"]
author = "tipobrata"
+++

## Bekerja dengan StrongLoop

Install strongloop

```
npm install -g strongloop
```

untuk membuat project jalan kan perintah di bawah: 
```
slc loopback
```

Buat nama applikasi dan folder applikasi sesuai yang di inginkan, pilih applikasi `hello-world`

ikuti langkah selanjutnya, membuat `model` dan menjalankannya: 

```
Next steps:

  Change directory to your app
    $ cd mei21

  Create a model in your app
    $ slc loopback:model

  Run the app
    $ node .
```

## Membuat Model

```
D:\Tools\loop\mei21>slc loopback:model
? Enter the model name: Cat
? Select the data-source to attach Cat to: db (memory)
? Select model's base class PersistedModel
? Expose Cat via the REST API? Yes
? Custom plural form (used to build REST URL): Cats
? Common model or server only? common
Let's add some Cat properties now.
```

**Menambah property
```
Enter an empty property name when done.
? Property name: name
   invoke   loopback:property
? Property type: string
? Required? No
? Default value[leave blank for none]:

Let's add another Cat property.
Enter an empty property name when done.
? Property name: color
   invoke   loopback:property
? Property type: string
? Required? No
? Default value[leave blank for none]:

Let's add another Cat property.
Enter an empty property name when done.
? Property name: age
   invoke   loopback:property
? Property type: number
? Required? No
? Default value[leave blank for none]:

Let's add another Cat property.
Enter an empty property name when done.
```

## Jalankan Server

```
D:\Tools\loop\mei21>node .
Web server listening at: http://localhost:3000
Browse your REST API at http://localhost:3000/explorer
```