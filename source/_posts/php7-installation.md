---
layout: post
title: "PHP7 Installation"
date:   2015-12-30
description: PHP7 Installation
categories: PHP
tags: php
---

* Get source code of php 7

```
wget http://cn2.php.net/distributions/php-7.0.1.tar.bz2
tar -xvf php-7.0.1.tar.bz2
```

* Install tools

```
sudo apt-get -y update
sudo apt-get -y install libxml2-dev
sudo apt-get -y install  build-essential
sudo apt-get -y install openssl 
sudo apt-get -y install libssl-dev 
sudo apt-get -y install make
sudo apt-get -y install curl
sudo apt-get -y install libcurl4-gnutls-dev
sudo apt-get -y install libjpeg-dev
sudo apt-get -y install libpng-dev
sudo apt-get -y install libmcrypt-dev
sudo apt-get -y install libreadline6 libreadline6-dev

```

* Compile

```
cd php-7.0.1/
./configure
./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --enable-fpm --with-fpm-user=www --with-fpm-group=www --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --with-mcrypt --enable-ftp --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-soap --without-pear --with-gettext --disable-fileinfo --enable-maintainer-zts
./configure --prefix=/usr/local/php --enable-fpm --enable-inline-optimization --disable-debug --disable-rpath --enable-shared --enable-opcache  --with-mysql --with-mysqli --with-mysql-sock  --enable-pdo --with-pdo-mysql --with-gettext --enable-mbstring --with-iconv --with-mcrypt --with-mhash --with-openssl --enable-bcmath --enable-soap --with-libxml-dir --enable-pcntl --enable-shmop --enable-sysvmsg --enable-sysvsem --enable-sysvshm --enable-sockets --with-curl --with-zlib --enable-zip --enable-bz2 --with-readline --without-sqlite3 --without-pdo-sqlite --with-pear --with-libdir=/lib/x86_64-linux-gnu --with-gd --with-jpeg-dir=/usr/lib --enable-gd-native-ttf --enable-xml
make && make test
make && sudo make install
```
* Config

```
cd /usr/local/php/etc/
cp php-fpm.conf.default php-fpm.conf
cp etc/php-fpm.d/www.conf.default etc/php-fpm.d/www.conf

#Change user & group in www.conf as follow:
#user = www-data
#group = www-data
```
* Start php-fpm

```
sudo /usr/local/php/sbin/php-fpm
```
* Add enviroment variable for php-cli

```
sudo echo "PATH=$PATH:/usr/local/php/bin">> /etc/profile
sudo echo "export PATH">> /etc/profile
source /etc/profile
```
