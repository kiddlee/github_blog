---
layout: post
title: "Laravel Seeder"
date:   2016-06-16
description: Laravel Seeder
categories: PHP
tags:
- php
- laravel
---

Seeder can create some fake data in table, **it's useful**.

* Create seeder

```
php artisan make:seeder ArticleSeeder
```
After that a file named *ArticleSeeder.php* would be created under **database/seeds**. Change function run as follow:

```
public function run()
{
    DB::table('articles')->delete();

    for ($i=0; $i < 10; $i++) {
        \App\Article::create([
            'title'   => 'Title '.$i,
            'body'    => 'Body '.$i,
            'user_id' => 1,
        ]);
    }
}
```

* Register seeder

Then we need register ArticleSeeder in project. Modify **function run** in file *database/seeds/DatabaseSeeder.php* as follow:

```
public function run()
{
    $this->call(ArticleSeeder::class);
}
```
* Excute seed and create fake data

Excuste seed with command 
```
php artisan db:seed
```
. You can get the fake data.
