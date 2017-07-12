## Laravel’s Directory Structure
- **app/** is where the bulk of your actual application will go. Models, controllers, route
definitions, commands, and your PHP domain code all go in here.
- **bootstrap/** contains the files that the Laravel framework uses to boot every time it runs.
- **config/** is where all the configuration files live.
- **database/** is where database migrations and seeds live.
- **public/** is the directory the server points to when it’s serving the website. This contains
index.php, which is the front controller that kicks off the bootstrapping process
and routes all requests appropriately. It’s also where any public-facing files
like images, stylesheets, scripts, or downloads go.
- **resources/** is where non-PHP files that are needed for other scripts live. Views, language
files, and (optionally) Sass/LESS and source JavaScript files live here.
- **routes/** is where all of the route definitions live, both for HTTP routes and “console
routes,” or Artisan commands.
- **storage/** is where caches, logs, and compiled system files live.
- **tests/** is where unit and integration tests live.
- **vendor/** is where Composer installs its dependencies. It’s Git-ignored (marked to
be excluded from your version control system), as Composer is expected to run
as a part of your deploy process on any remote servers.
- **env** and **.env.example** are the files that dictate the environment variables (variables
that are expected to be different in each environment and are therefore not
committed to version control). .env.example is a template that each environment
should duplicate to create its own .env file, which is Git-ignored.
- **artisan** is the file that allows you to run Artisan commands (see Chapter 7) from
the command line.
- **gitignore** and **.gitattributes** are Git configuration files.
- **composer.json** and composer.lock are the configuration files for Composer; composer.
json is user-editable and composer.lock is not. These files share some basic
information about this project and also define its PHP dependencies.
- **gulpfile.js** is the (optional) configuration file for Elixir and Gulp. This is for
compiling and processing your frontend assets.
- **package.json** is like composer.json but for frontend assets.
- **phpunit.xml** is a configuration file for PHPUnit, the tool Laravel uses for testing
out of the box.
- **readme.md** is a Markdown file giving a basic introduction to Laravel.
