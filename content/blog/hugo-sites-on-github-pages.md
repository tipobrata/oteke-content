+++
title = "Hugo Sites On Github"
date = "2017-07-28T21:49:20+02:00"
tags = ["hugo"]
categories = ["hugo"]
author = "tipobrata"
+++

## Buat Blog Hugo
```
$ hugo new site sample-hugo

Congratulations! Your new Hugo site is created in /home/nagamaska/Tools/Hugo/project/sample-hugo.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/, or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation

```

## Buat post pada blog hugo

```
hugo new post/satu-post.md

sample-hugo/content/post/satu-post.md created

```

## masuk ke directory project

```
cd sample-hugo
```

## Jalankan init pada project

```
$ git init

Initialized empty Git repository in /home/nagamaska/Tools/Hugo/project/sample-hugo/.git/

```

## Tambahkan themes dari repository git

```
git submodule add https://github.com/Vimux/Mainroad.git themes/mainroad

Cloning into 'themes/hurock'...
remote: Counting objects: 237, done.
remote: Total 237 (delta 0), reused 0 (delta 0), pack-reused 237
Receiving objects: 100% (237/237), 2.69 MiB | 559.00 KiB/s, done.
Resolving deltas: 100% (109/109), done.
Checking connectivity... done.

```

## edit example road

```
$ hugo serve
```

buka browser, jika belum muncul jalankan perintah di bawah

```
$ cp themes/mainroad/exampleSite/* . -r

```

## Menampilkan post yang di buat

post yang kita buat masih belum tampil, untuk menampilkan post yang `draft:"true"` jalankan perintah di bawah.

```
hugo undraft content/post/satu-post.md 

```

## Hosting di github

buat repository di github dengan nama `sample-hugo`
masih di dalam folder project, untuk meremote repository yang sudah di buat, menggunakan perintah:

```
git remote add origin xxx@xxxurlgit

```
untuk perintah lengkapnya

```
git remote add origin git@github.com:tipobrata/sample-hugo.git

```

Jalankan git status

```
$ git status

On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .gitmodules
	new file:   themes/hurock
	new file:   themes/mainroad

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	config.toml
	content/
	data/
	static/

```

jalankan git All

```
$ git add --all

```

Jalankan git commit

```
$ git commit -m "initial commit"
```

Jalankan push, saat menjalankan push,akan minta password pashpress yang skita buat tadi saat create ssh keys

```
$ git push -u origin master

Counting objects: 11, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (11/11), 1.83 KiB | 0 bytes/s, done.
Total 11 (delta 0), reused 0 (delta 0)
To git@github.com:tipobrata/sample-hugo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```
##  Cara Build Hugo menjadi website

masih dalam folder project build hugo menjadi website dan akan terbentuk folder `public`
```
$ hugo

Started building sites ...
Built site for language en:
0 draft content
0 future content
0 expired content
2 regular pages created
8 other pages created
0 non-page files copied
2 paginator pages created
0 tags created
0 categories created
total in 18 ms

```
pada `config.toml` tambahkan baris di bawah, kemudian generate build pada hugo dengan perintah `hugo` dalam folder project

## Deploy Hugo ke directory `docs`

```
baseurl = "https://tipobrata.github.io/sample-hugo/"
publishDir = "docs"
```


sebelum kita push ke github pages hapus terlebih dahulu folder `public` 

```
$ rm -r pubilc/
$ git status
$ git add --all
$ git commit -m "commit url"
$ git push
```
login ke web github pada Repository `sample-hugo` klik => `setting -> options -> GitHub Pages` rubah ke folder `docs`


## Deploy ke username.github.io

Buat repository dengan nama `username.github.io`, buat sub module / repository remote di github di dengan command di bawah:

```
git submodule add -b master git@github.com:username/username.github.io.git public
```

push ke repository

```
$ git add .
$ git commit -m "keterangan commit"
$ git push -u origin master

```
Buat folder file `deploy.sh` dalam folder blog dan jalankan script `deploy.sh`

```
$ ./deploy.sh 
Deploying updates to GitHub...
Started building sites ...
Built site for language en:
0 draft content
0 future content
0 expired content
12 regular pages created
40 other pages created
0 non-page files copied
18 paginator pages created
6 categories created
10 tags created
total in 277 ms
[master fd78844] rebuilding site Sun 30 Jul 07:51:40 WIB 2017
 36 files changed, 77 insertions(+), 602 deletions(-)
Counting objects: 88, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (70/70), done.
Writing objects: 100% (88/88), 23.13 KiB | 0 bytes/s, done.
Total 88 (delta 35), reused 0 (delta 0)
remote: Resolving deltas: 100% (35/35), completed with 25 local objects.
To git@github.com:tipobrata/tipobrata.github.io.git
   a0fb417..fd78844  master -> master

```