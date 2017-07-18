## Route Groups
Route groups allow you to group several routes together, and apply any shared configuration
settings once to the entire group, to reduce this duplication. Additionally,
route groups are visual cues to future developers (and to your own brain) that these
routes are grouped together. 

Pass a closure to the group definition, and defining the grouped routes within that closure:
```php
Route::group([], function () {
  Route::get('hello', function () {
    return 'Hello';
  });
  Route::get('world', function () {
    return 'World';
  });
});
```
By default, a route group doesn’t actually do anything.

### Middleware
Probably the most common use for route groups is to apply middleware to a group of
routes. Laravel uses it for authenticating users and restricting guest users from
using certain parts of a site.

In this example, it means users have
to be logged in to the application to view the dashboard or the account page:
```php
Route::group(['middleware' => 'auth'], function () {
  Route::get('dashboard', function () {
    return view('dashboard');
  });
  Route::get('account', function () {
    return view('account');
  });
});
```
Often it’s clearer and more direct to attach middleware to your
routes in the controller instead of at the route definition. You can
do this by calling the `middleware()` method in the constructor of
your controller:
```php
class DashboardController extends Controller {
  public function __construct() {
    $this->middleware('auth');
    $this->middleware('admin-auth')->only('admin');
    $this->middleware('team-member')->except('admin');
  }
}
```
Note that, if you’re doing a lot of “only” and “except” customizations,
that’s often a sign that you should break out a new controller
for the exceptional routes.

### Path Prefixes
If you have a group of routes that share a segment of their path—for example, if your
site’s API is prefixed with `/api` — you can use route groups to simplify this structure:
```php
Route::group(['prefix' => 'api'], function () {
  Route::get('/', function () {
    // Handles the path /api
  });
  Route::get('users', function () {
    // Handles the path /api/users
  });
});
```

### Subdomain Routing
Subdomain routing is the same as route prefixing, but it’s scoped by subdomain
instead of route prefix. There are two primary uses for this. First, you may want to
present different sections of the application (or entirely different applications) to different
subdomains:
```php
Route::group(['domain' => 'api.myapp.com'], function () {
  Route::get('/', function () {
  //
  });
});
```
Second, you might want to set part of the subdomain as a parameter. This is most often done in cases of 
multitenancy (think Slack or Harvest, where each company gets its own subdomain:
```php
Route::group(['domain' => '{account}.myapp.com'], function () {
  Route::get('/', function ($account) {
    //
  });
  Route::get('users/{id}', function ($account, $id) {
    //
  });
});
```

### Namespace Prefixes
When you’re grouping routes by subdomain or route prefix, it’s likely their controllers
have a similar PHP namespace. By using the route group namespace
prefix, you can avoid long controller references in groups
like `"API/ControllerA@index"` and `"API/ControllerB@index"`:
```php
// App\Http\Controllers\ControllerA
Route::get('/', 'ControllerA@index');

Route::group(['namespace' => 'API'], function () {
  // App\Http\Controllers\API\ControllerB
  Route::get('api/', 'ControllerB@index');
});
```
### Name Prefixes
The prefixes don’t stop there. It’s common that route names will reflect the inheritance
chain of path elements, so `users/comments/5` will be served by a route named
`users.comments.show`. In this case, it’s common to use a route group around all of
the routes that are beneath the users.comments resource:
```php
Route::group(['as' => 'users.', 'prefix' => 'users'], function () {
  Route::group(['as' => 'comments.', 'prefix' => 'comments'], function () {
    // Route name will be users.comments.show
    Route::get('{id}', function () {
      //
    })->name('show');
  });
});
```
