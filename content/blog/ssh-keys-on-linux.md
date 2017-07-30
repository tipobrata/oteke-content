+++
title = "Menggunakan Ssh"
date = "2017-07-06T21:49:20+02:00"
tags = ["ssh", "linux"]
categories = ["linux"]
author = "tipobrata"
+++


## Cara mengecek key rsa yang sudah di ada
```
$ ls -al ~/.ssh
```

## Cara membuat `ssh Keys` dengan ssh

```
$ ssh-keygen -t rsa -b 4096 -C "xperia.tipobrata@gmail.com"

Generating public/private rsa key pair.
Enter file in which to save the key (/home/nagamaska/.ssh/id_rsa):
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/nagamaska/.ssh/id_rsa.
Your public key has been saved in /home/nagamaska/.ssh/id_rsa.pub.
The key fingerprint is:
31:1e:74:a3:dc:17:cd:5a:a9:5d:4c:28:c1:a9:28:c8 xperia.tipobrata@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|        . o.o= =.|
|       o + .+.* o|
|   . .  *....* . |
|    E ...+..o .  |
|       .S        |
|                 |
|                 |
|                 |
|                 |
+-----------------+

```

## cara copy public key ssh dengan command prompt

```
$ sudo apt-get install xclip

# Copies the contents of the id_rsa.pub file to your clipboard
$ xclip -sel clip < ~/.ssh/id_rsa.pub

```

## Menambahkan ssh keys ke ssh agent

pertama-tama jalankan `ssh-agent` secara background

Cara menjalankan `ssh agent` secara background

```
$ eval "$(ssh-agent -s)"

```

cara menambahkan `ssh keys` private ke `ssh-agent`

```
$ ssh-add ~/.ssh/id_rsa

Enter passphrase for /home/xxxx/.ssh/id_rsa: 
Identity added: /home/xxxx/.ssh/id_rsa (/home/nagamaska/.ssh/id_rsa)

```