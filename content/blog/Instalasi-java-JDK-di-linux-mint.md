+++
title = "Startup Java On Linux Mint"
date = "2017-05-22T21:49:20+02:00"
tags = ["lmde", "linux"]
categories = ["linux"]
author = "tipobrata"
+++

### Instalasi JDK 8 di Linux Mint

Download JDK sesuai OS

[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

```
$ file /sbin/init
/sbin/init: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=e8b7c47e46abe359442f435fc95144279c5ddec5, stripped

```
### Cek java version

```
$ java -version
java version "1.7.0_111"
OpenJDK Runtime Environment (IcedTea 2.6.7) (7u111-2.6.7-2~deb8u1)
OpenJDK 64-Bit Server VM (build 24.111-b01, mixed mode)

```
### Cara Hapus OpenJDK yang sudah terinstall

```
$ sudo apt-get purge openjdk-* 
```

**Buat directory java**

```
$ sudo mkdir -p /usr/local/java
$ sudo cp -r jdk-8u60-linux-x64.tar.gz /usr/local/java/
$ cd /usr/local/java

```

- Extract Paket Binary Java

```
sudo tar xvzf jdk-8u60-linux-x64.tar.gz
```

- Menambahkan PATH Environment pada system

PATH file /etc/profile dan tambahkan variable sistem berikut untuk jalur sistem. Gunakan gedit atau text editor lainnya.

```
sudo gedit /etc/profile

JAVA_HOME=/usr/local/java/jdk1.8.0_131
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
export JAVA_HOME
export PATH

```


- Perintah untuk memberitahukan sistem bahwa Oracle Java JRE tersedia untuk digunakan.

```
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/local/java/jdk1.8.0_131/bin/java" 1

```

- Perintah ini memberitahukan sistem bahwa Oracle Java JDK tersedia untuk digunakan.

```
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/local/java/jdk1.8.0_131/bin/javac" 1
```

- Perintah ini memberitahukan sistem bahwa Oracle Java Web Start tersedia untuk digunakan.

```
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/local/java/jdk1.8.0_131/bin/javaws" 1

```

### Memberitahu sistem bahwa Oracle Java JDK/JRE harus menjadi default Java.

Set JRE:

```
sudo update-alternatives --set java /usr/local/java/jdk1.8.0_131/bin/java
```

- Set Javac Compiler

```
sudo update-alternatives --set javac /usr/local/java/jdk1.8.0_131/bin/javac
```

- Set Java Web Start

```
sudo update-alternatives --set javaws /usr/local/java/jdk1.8.0_131/bin/javaws 
```

- Reload system wide PATH /etc/profile dengan perintah:

```
. /etc/profile
```

- Tes untuk melihat apakah Oracle Java telah terinstal

```
java -version
```


### Install Netbean 8.2

[NetBean Download](https://netbeans.org/downloads/index.html)

Masuk ke directory file yang terdownload, kemudian berikan hak akses execute dan jalankan execute, dengan perintah di bawah:

```
$ chmod +x netbeans-8.2-linux.sh
$ sh ./netbeans-8.2-linux.sh
```

### Install Maven


[Maven 3.5.0](http://apache.repo.unpas.ac.id/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz)


Copy file maven yang sudah di download ke directory `opt`

```
sudo cp -r apache-maven-3.5.0-bin.tar.gz /opt/
```

Masuk kedirectory opt, dan jalankan : 

```
tar xzvf apache-maven-3.5.0-bin.tar.gz
```


Check environment variable value

```
echo $JAVA_HOME
```

- Adding to PATH

```
export PATH=/opt/apache-maven-3.5.0/bin:$PATH
```

**Menambahkan maven variabel secara permanent**

Atau `$ sudo gedit /etc/profile`


```
M2_HOME=/opt/apache-maven-3.3.9
export M2_HOME
M2=$M2_HOME/bin

PATH=$PATH:$M2
export PATH
```

Reload system ketik: ‘source /etc/profile’

- Test Installation

```
 $ mvn –version
```

### Install MySQl 5.7 di debian 8 dengan menggunakan APT Repository

Download deb dpkg

```
wget https://dev.mysql.com/get/mysql-apt-config_0.8.5-1_all.deb
```

Install dpkg mySQL
```
sudo dpkg -i mysql-apt-config_0.8.5-1_all.deb
```

```
sudo apt-get update
```

Install the server

```
apt-get install mysql-community-server
```

masukkan password root dan ikuti instalasi sampai selesai.


test login ke mysql menggunakan user root
```
mysql -u root -p

```

membuat database
```
create database testdb;
```

membuat user di MySql dengan nama `testuser`

```
create user 'testuser'@'localhost' identified by 'password';
```

Memberikan akses database `testdb` ke user `testuser` 

```
grant all on testdb.* to 'testuser' identified by 'password';

```

Menggunakan user `testuser` untuk akses ke db `testdb` dan membuat table

```
mysql -u testuser -p
use testdb;

create table customers (customer_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, first_name TEXT, last_name TEXT);

```

Cara Stop the current MySQL server instance.

```
sudo systemctl stop mysql.service
```

Install Tune MySQL

```
sudo apt-get install mysqltuner
```

Cara menjalankannya
```
mysqltuner
```

Akan muncul untuk login password di bawah
```
Please enter your MySQL administrative login:
Please enter your MySQL administrative password:
```

MySql config file berada `/etc/mysql/my.cnf`
 MySql se
cara stop, start dan restart MySQL setelah merubah config, jalankan perintah di bawah :

```
sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start
sudo /etc/init.d/mysql restart
```

### Install Tomcat 8.5.x di debian jessy

[Install Tomcat](https://wolfpaulus.com/java/tomcat-jessie/)

[debian tutorial](http://www.debiantutorials.com/category/web/)

Ketikkan bash di bawah
```
nagamaska@oteke /home $ sudo adduser \
> --system \
> --shell /bin/bash \
> --gecos 'Tomcat Java Servlet and JSP engine' \
> --group \
> --disabled-password \
> --home /home/tomcat \
> tomcat
[sudo] password for nagamaska: 
Adding system user `tomcat' (UID 121) ...
Adding new group `tomcat' (GID 133) ...
Adding new user `tomcat' (UID 121) with group `tomcat' ...
Creating home directory `/home/tomcat' ...

```

- Download dan extrak paket tomcat 8

```
$ wget http://www.us.apache.org/dist/tomcat/tomcat-8/v8.5.5/bin/apache-tomcat-8.5.5.tar.gz
$ tar xvzf ./apache-tomcat-8.5.5.tar.gz
$ rm ./apache-tomcat-8.5.5.tar.gz
$ sudo mv ./apache-tomcat-8.5.5 /usr/share
```

To make it easy to replace this release with future releases, we are going to create a symbolic link that we are going to use when referring to Tomcat (after removing the old link, you might have from installing a previous version):

```
$ sudo rm -f /usr/share/tomcat
$ sudo ln -s /usr/share/apache-tomcat-8.5.5 /usr/share/tomcat
```
If Tomcat’s default HTTP port (8080) is already in use, you need to edit the server.xml configuration file, e.g.
edit /usr/share/tomcat/conf/server.xml and replace 8080 with 8000

```
$ sudo chown -R tomcat:tomcat /usr/share/tomcat/*
$ sudo chmod +x /usr/share/tomcat/bin/*.sh

```

- Starting Tomcat

```
$ sudo /bin/su - tomcat -c /usr/share/tomcat/bin/startup.sh
Using CATALINA_BASE:   /usr/share/tomcat
Using CATALINA_HOME:   /usr/share/tomcat
Using CATALINA_TMPDIR: /usr/share/tomcat/temp
Using JRE_HOME:        /usr/local/java/jdk1.8.0_131
Using CLASSPATH:       /usr/share/tomcat/bin/bootstrap.jar:/usr/share/tomcat/bin/tomcat-juli.jar
Tomcat started.

```

- Stopping Tomcat

```
$ sudo /bin/su - tomcat -c /usr/share/tomcat/bin/shutdown.sh
Using CATALINA_BASE:   /usr/share/tomcat
Using CATALINA_HOME:   /usr/share/tomcat
Using CATALINA_TMPDIR: /usr/share/tomcat/temp
Using JRE_HOME:        /usr/local/java/jdk1.8.0_131
Using CLASSPATH:       /usr/share/tomcat/bin/bootstrap.jar:/usr/share/tomcat/bin/tomcat-juli.jar

```

- Menjalankan server tomcat pada saat booting pertama kali

```
#!/bin/bash
 
### BEGIN INIT INFO
# Provides:        tomcat
# Required-Start:  $network
# Required-Stop:   $network
# Default-Start:   2 3 4 5
# Default-Stop:    0 1 6
# Short-Description: Start/Stop Tomcat server
### END INIT INFO
 
PATH=/sbin:/bin:/usr/sbin:/usr/bin
 
start() {
 /bin/su - tomcat -c /usr/share/tomcat/bin/startup.sh
}
 
stop() {
 /bin/su - tomcat -c /usr/share/tomcat/bin/shutdown.sh 
}
 
case $1 in
  start|stop) $1;;
  restart) stop; start;;
  *) echo "Run as $0 &lt;start|stop|restart&gt;"; exit 1;;
esac
```

dan rubah permission symlink automatis

```
chmod 755 /etc/init.d/tomcat
update-rc.d tomcat defaults
```

### Install IntelliJ IDEA

Download IntelliJ IDEA [ideaIC-2017.1.2.tar.gz](https://www.jetbrains.com/idea/download/download-thanks.html?platform=linux&code=IIC)

* Copy hasil download ke directory `opt`

```
$ sudo tar xf <ideaIC or ideaIU>-*.tar.gz -C /opt/

```

* Masuk ke directory `opt`

```
cd opt/<ideaIC or ideaIU>-*/bin

```

* Jalankan `idea.sh` dalam `/bin` subdirectory contoh: `/opt/idea-IC-171.4249.39/bin`

```
$ sh ./idea.sh
```

Selanjutnya ikuti instalasi seperti biasa.


### Install Android Studio

Extract `android-studio-ide-162.4069837-linux.zip` ke dalam folder `/opt`

```
$ sudo unzip android-studio-ide-141.2178183-linux.zip -d /opt/
```

Masuk ke directory di bawah
```
$ cd /opt/android-studio/bin
```
Jalankan command di bawah untuk menjalankan instalasi

```
$ ./studio.sh
```
Selanjutnya ikuti instalasi seperti biasa.

- install plugin yang berhubungan dengan kotlin

### Install MongoDB

[install mongoDB](https://www.hugeserver.com/kb/install-mongodb-debian-8-ubuntu-16/)
[mongoDB DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-debian-8)

tambahkan

```
#security:
security:
 authorization: enabled
```

Manage your MongoDB Service

```
# systemctl enable mongod
```

For Start/Stop MongoDB serivce:

```
# systemctl start mongod

# systemctl stop mongod

or

# service mongod start

# service mongod stop
```

See your MongoDB status:

```
# systemctl status mongod
```