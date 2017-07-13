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
Note that we `return` our content and don’t `echo` or `print` it:
```
Route::get('/', function () {
  return view('welcome');
});

Route::get('about', function () {
  return view('about');
});
```
If you have much experience developing PHP, you might be surprised
to see static calls on the Route class. This is not actually a
static method per se, but rather service location using Laravel’s
facades.
If you prefer to avoid facades, you can accomplish these same definitions like this:
```
$router->get('/', function () {
  return 'Hello, World!';
});
```
### Route Verbs
You might’ve noticed that we’ve been using `Route::get` in our route definitions. This
means we’re telling Laravel to only match for these routes when the HTTP request
uses the GET action. There are a few other options for methods to call on a route
definition:
```
Route::get('/', function () {
  return 'Hello, World!';
});

Route::post('/', function () {});

Route::put('/', function () {});

Route::delete('/', function () {});

Route::any('/', function () {});

Route::match(['get', 'post'], '/', function () {});
```
### Route Handling
The other common option is to pass a controller name and method as a string in
place of the closure:
```
Route::get('/', 'WelcomeController@index');
```
This is telling Laravel to pass requests to that path to the `index()` method of the App
`\Http\Controllers\WelcomeController` controller. This method will be passed the
same parameters and treated the same way as a closure you might’ve alternatively put
in its place.
### Route Parameters
If the route you’re defining has parameters—segments in the URL structure that are
variable—it’s simple to define them in your route and pass them to your closure:
```
Route::get('users/{id}/friends/{order]', function ($id, $order) {
  //
});
```
You can also make your route parameters optional by including a question mark (?)
after the parameter name. In this case, you should also
provide a default value for the route’s corresponding variable.
```
Route::get('users/{id?}', function ($id = 'fallbackId') {
  //
});
```
And you can use regular expressions (regexes) to define that a route should only
match if a parameter meets particular requirements:
```
Route::get('users/{id}', function ($id) {
  //
})->where('id', '[0-9]+');
```
### Route Names
The simplest way to refer to these routes elsewhere in your application is just by their
path. There’s a `url()` helper to simplify that linking in your views:
```php
<a href="<?php echo url('/'); ?>">
// outputs href="http://myapp.com/"
```
However, Laravel also allows you to name each route, which enables you to refer to it
without explicitly referencing the URL. This is helpful because it means you can give
simple nicknames to complex routes, and also because linking them by name means
you don’t have to rewrite your frontend links if the paths change:
```
// Defining a route with name in routes/web.php:
Route::get('members/{id}', 'MembersController@show')->name('members.show');
// Link the route in a view using the route() helper
<a href="<?php echo route('members.show', ['id' => 14]); ?>">
```
Fluent route definitions don’t exist in Laravel 5.1. You’ll need to
instead pass an array to the second parameter of your route definition:
```
Route::get('members/{id}', [
  'as' => 'members.show',
  'uses' => 'MembersController@show'
]);
```
### Route Naming Conventions
You can name your route anything you’d like, but the common convention is to use
the plural of the resource name, then a period, then the action. So, here are the routes
most common for a resource named photo:
```
photos.index
photos.create
photos.store
```
