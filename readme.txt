Local: /Users/mohammadselimmiah/Sites/Api/ApiSitepoint/laravel-api-boilerplate-jwt

https://www.sitepoint.com/how-to-build-an-api-only-jwt-powered-laravel-app/
git clone https://github.com/francescomalatesta/laravel-api-boilerplate-jwt
          https://github.com/francescomalatesta/laravel-api-boilerplate-angular-example.git
composer install
edit .env file
create database and configure .env
php artisan migrate
php artisan serve
==============================================
use postman:
http://localhost:8000/api/auth/signup
POST method
body=>form-data
Text=>name
Text=>email
Text=>password
Send
User will be created in the database.

Now try to login:
http://localhost:8000/api/auth/login
POST=> email, password
Send

====================================================
php artisan make:migration create_books_table --create=books

    public function up()
    {
        Schema::create('books', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title');
            $table->string('author_name');
            $table->integer('pages_count');
            $table->integer('user_id')->index();
            $table->timestamps();
        });
    }

$ php artisan migrate

$ php artisan make:model Book

protected $fillable = ['title', 'author_name', 'pages_count'];

in the User model,

public function books()
{
    return $this->hasMany('App\Book');
}

$ php artisan make:controller BookController

move it to app/Api/V1/Controllers.

$api->group(['middleware' => 'api.auth'], function ($api) {
	$api->post('book/store', 'App\Api\V1\Controllers\BookController@store');
	$api->get('book', 'App\Api\V1\Controllers\BookController@index');
});


use postman:
http://localhost:8000/api/book/store?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEsImlzcyI6Imh0dHA6XC9cL2xvY2FsaG9zdDo4MDAwXC9hcGlcL2F1dGhcL2xvZ2luIiwiaWF0IjoxNDcwMTg0NzM0LCJleHAiOjE0NzAxODgzMzQsIm5iZiI6MTQ3MDE4NDczNCwianRpIjoiMjUwYjBhNDQ2MGYzZWQxNWNhZmEwNTIxYjE4Zjg5MjcifQ.hg3xA4WS4q-ZagbsuI5UGVjLadDyOCAKbYzL6Vi2hnI
title
author_name
pages_count

http://localhost:8000/api/free

$ php artisan api:routes
+------+-------------------------+------+------------------------------------------------+-----------+------------+----------+------------+
| Host | URI                     | Name | Action                                         | Protected | Version(s) | Scope(s) | Rate Limit |
+------+-------------------------+------+------------------------------------------------+-----------+------------+----------+------------+
|      | POST /api/auth/login    |      | App\Api\V1\Controllers\AuthController@login    | No        | v1         |          |            |
|      | POST /api/auth/signup   |      | App\Api\V1\Controllers\AuthController@signup   | No        | v1         |          |            |
|      | POST /api/auth/recovery |      | App\Api\V1\Controllers\AuthController@recovery | No        | v1         |          |            |
|      | POST /api/auth/reset    |      | App\Api\V1\Controllers\AuthController@reset    | No        | v1         |          |            |
|      | GET|HEAD /api/protected |      | Closure                                        | Yes       | v1         |          |            |
|      | GET|HEAD /api/free      |      | Closure                                        | No        | v1         |          |            |
|      | POST /api/book/store    |      | App\Api\V1\Controllers\BookController@store    | Yes       | v1         |          |            |
|      | GET|HEAD /api/book      |      | App\Api\V1\Controllers\BookController@index    | Yes       | v1         |          |            |
+------+-------------------------+------+------------------------------------------------+-----------+------------+----------+------------+