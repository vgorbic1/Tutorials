## Views
Views (or templates) are files that describe what some particular output should look like. You
might have views for JSON or XML or emails, but the most common views in a web
framework output HTML.

In Laravel, there are two formats of view you can use out of the box: plain PHP, or
Blade templates. The difference is in the filename: about.php will
be rendered with the PHP engine, and about.blade.php will be rendered with the
Blade engine.

Once you’ve loaded a view, you have the option to simply return it, which will 
work fine if the view doesn’t rely on any variables from the controller.
```php
Route::get('/', function () {
  return view('home');
});
```
This code looks for a view in `resources/views/home.blade.php` or `resources/views/
home.php`, and loads its contents and parses any inline PHP or control structures until
you have just the view’s output. Once you return it, it’s passed on to the rest of the
response stack and eventually returned to the user.

### Passing Variables to Views
```php
Route::get('tasks', function () {
  return view('tasks.index')->with('tasks', Task::all());
});
```
This closure loads the `resources/views/tasks/index.blade.php` or `resources/views/tasks/
index.php` view and passes it a single variable named `tasks`, which contains the result
of the `Task::all()` method. `Task::all()` is an Eloquent database query.
