## Routes
In a Laravel application, you will define your “web” routes in `routes/web.php` and your
“API” routes in `routes/api.php`. Web routes are those that will be visited by your end
users; API routes are those for your API, if you have one.

In projects running versions of Laravel prior to 5.3, there will be
only one routes file, located at `app/Http/routes.php`.

Use a closure for a basic route definition:
```
// routes/web.php
Route::get('/', function () {
  return 'Hello, World!';
});
```
