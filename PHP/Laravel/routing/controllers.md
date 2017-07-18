## Controllers
Controllers tend to group similar routes together, especially if your application
is structured along a traditionally CRUD-like format; in this case, a controller
might handle all the actions that can be performed on a particular resource.

A controller’s primary job is to capture the
intent of an HTTP request and pass it on to the rest of the application.

To create a controller use Artisan (Artisan comes with Laravel) with the folloing command:
```
php artisan make:controller NameOfTheController
```
