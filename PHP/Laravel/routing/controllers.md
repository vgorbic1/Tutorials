## Controllers
Controllers tend to group similar routes together, especially if your application
is structured along a traditionally CRUD-like format; in this case, a controller
might handle all the actions that can be performed on a particular resource.

A controller’s primary job is to capture the
intent of an HTTP request and pass it on to the rest of the application.

To create a controller use Artisan (Artisan comes with Laravel) from the project root with the folloing command:
```
php artisan make:controller TaskController
```
The following code will be generated in `app/Http/Controllers/TasksController.php`:
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Http\Requests;

class TasksController extends Controller { }
```
To return a *Hello, World!* string modify the code:
```php
<?php
use App\Http\Controllers;
class TasksController extends Controller {
  public function home() {
    return 'Hello, World!';
  }
}
```
Create a route for this controller in `routes/web.php`:
```php
<?php
  Route::get('/', 'TasksController@home');
```
Visit the `/` route and you’ll see the words "Hello, World!"

We can ignore the `App\Http\Controllers\` when we reference controllers, because by default, Laravel
is configured to look for controllers within that namespace. This means that if you have a controller 
with the fully qualified class name of `App\Http\Controllers\API\ExercisesController`, you’d reference 
it in a route definition as `API\ExercisesController`.

### Common controller method example
```php
// TasksController.php
...
public function index()
{
return view('tasks.index')
->with('tasks', Task::all());
}
```
This controller method loads the `resources/views/tasks/index.blade.php` or `resources/
views/tasks/index.php` view and passes it a single variable named `tasks`, which contains
the result of the `Task::all()` Eloquent method.
