---
layout: post
title: "How to create a SSL Certificate with nginx"
date:   2016-06-19
description: How to create a SSL Certificate with nginx
categories: Nginx
tags:
- nginx
- ssl
---

* Create a folder to hold all of SSL information

```
sudo mkdir /etc/nginx/ssl
```
* Create the SSL key and certificate file

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt
```
* Config nginx as follow:

```
server {
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        listen 443 ssl;

        root /usr/share/nginx/html;
        index index.html index.htm;

        server_name your_domain.com;
        ssl_certificate /etc/nginx/ssl/nginx.crt;
        ssl_certificate_key /etc/nginx/ssl/nginx.key;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
* Restart nginx service

[How To Create an SSL Certificate on Nginx for Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-create-an-ssl-certificate-on-nginx-for-ubuntu-14-04)