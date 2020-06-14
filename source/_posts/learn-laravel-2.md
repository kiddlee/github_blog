---
layout: post
title: "learn laravel 2"
date:   2015-09-07
description: learn laravel 2
categories: PHP
tags:
- php
- laravel
---

## Data Migrations
* Create a migration

	```
	php artisan make:migration create_users_table
	
	or
	
	php artisan make:migration add_votes_to_users_table --table=users
	php artisan make:migration create_users_table --create=users
	```
* Run migration

	```
	php artisan migrate
	```
* Check migrate status

	```
	php artisan migrate:status
	```
* Add Foreign Key

	```
	$table->integer('user_id')->unsigned();
   $table->foreign('user_id')->references('id')->on('users');
	```