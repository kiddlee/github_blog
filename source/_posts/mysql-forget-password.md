---
layout: post
title: "Forget Mysql password"
date:   2016-01-19
description: Forget Mysql password
categories: DataBase
tags: mysql
---

Forget mysql password

* Edit config of mysql, like /etc/mysql/my.conf
* Add skip-grant-tables in block [mysqld]
* Restart mysql, and then you can access mysql without password
* Update password

```
update mysql.user  set password=password('newpassword') where user='<username>'
``` 
* Then edit mysql config and delete skip-grant-tables
* Restart mysql

Then you can access mysql with new password
