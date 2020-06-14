---
layout: post
title: "Create Site"
date:   2015-03-24
description: Create Web Site Base On Laravel5
categories: PHP
tags: 
- php
- laravel
---

* Create project

```
composer create-project laravel/laravel learnlaravel5
```
* Launch project

```
php -S 0.0.0.0:1234

```
Then you can see the site with http://localhost:1234

* Add simple auth

```
php artisan make:auth
```
Add you can see the page as follow:

![add auth](source/posts/images/1/1.jpg)

Then you need create database, configurate database .env file & migrate. 

migrate command: 
```
php artisan migrate
```
. Now you can register and login the system, but the home page need customer login. That because **HomeController function __construct** add auth as follow:

```
public function __construct()
{
    $this->middleware('auth');
}
```
Then we need change in file *app/Http/Controllers/Auth/AuthController.php*
```
protected $redirectTo = 'admin';
```. Sometimes our home page need show to every customer, so just delete this construct.

* Add model

```
php artisan make:model ModelName
```
Then you will get a model class under folder app as follow:

```
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class ModelName extends Model
{
    //
}
```
* Create table for model

```
php artisan make:migration create_modelname_table
```
Then a file named ****\_create\_modelname\_table would be created under folder database/migrations. Modify the function up as follow:

```
public function up()
{
    Schema::create('articles', function(Blueprint $table)
    {
        $table->increments('id');
        $table->string('title');
        $table->text('body')->nullable();
        $table->integer('user_id');
        $table->timestamps();
    });
}
```
Then migrant again with
```
php artisan migrate
```
You can see the table in database;

* Add controller

```
php artisan make:controller SubFolder/NameController
```
After that the contorller would be created under app/Http/Controllers. Add the function in the controller as follow: 

```
public function index()
{
    return view('admin/article/index')->withArticles(Article::all());
}
```
For this controller, you need add *index.blade.php* under *resources/views/admin/article* to show data. If use the model in controller, you need add
```
use App\Model;
```
in the controller.

* Add Router

Add router for admin model, we need configurate auto and namespace as follow:

```
Route::group(['middleware' => 'auth', 'namespace' => 'Admin', 'prefix' => 'admin'], function() {
    Route::get('/', 'HomeController@index');
    Route::get('article', 'ArticleController@index');
});
```

If you need search, get, update & delete router, you can add router as follow:

```
Route::resource('article', 'ArticleController');
```
It's resource control in laravel, you will get 7 routes in project:

|verb|path|action|
|----|----|----|
|GET|/article|index|
| GET |/article/create|create|
|POST|/article|store|
| GET |/article/{article}|show|
| GET |/article/{article}/edit|edit|
|PUT/PATCH|/article/{article}|update|
|DELETE|/article/{article}|delete|




[example code](source/posts/code/1/learnlaravel5.tgz)
