---
layout: post
title: "Linux安全初始化"
date:   2016-02-29
description: Linux安全初始化
categories: Linux
tags:
- linux
- security
---

- 创建一个deploy的非根用户并加入sudo用户组

```
adduser deploy
usermod -a -G sudo deploy
```
- ssh密钥对认证

```
#在本地生成密钥
ssh-keygen
#copy到服务器
ssh-copy-id -i ~/.ssh/id_rsa.pub root@<serverip>
```
- 禁用密码，禁止root登录，编辑 /etc/ssh/sshd_config 文件，找到PasswordAuthentication设置，改为no，找到PermitRootLogin设置，改为no，重启ssh服务

```
sudo service ssh restart
```

