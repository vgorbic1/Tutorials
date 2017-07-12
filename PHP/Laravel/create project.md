## Creating a New Laravel Project

There are two ways to create a new Laravel project, but both are run from the command
line. The first option is to globally install the Laravel installer tool (using Composer);
the second is to use Composer’s `create-project` feature.

### Installing Laravel with the Laravel Installer Tool
If you have Composer installed globally, installing the Laravel installer tool is as simple
as running the following command:
```
composer global require "laravel/installer=~1.1"
```
Once you have the Laravel installer tool installed, spinning up a new Laravel project
is simple. Just run this command from your command line:
```
laravel new projectName
```
This will create a new subdirectory of your current directory named projectName and
install a bare Laravel project in it.

### Installing Laravel with Composer’s create-project Feature
Composer also offers a feature called create-project for creating new projects with
a particular skeleton. To use this tool to create a new Laravel project, issue the following
command:
```
composer create-project laravel/laravel projectName --prefer-dist
```
Just like the installer tool, this will create a subdirectory of your current directory
named projectName that contains a skeleton Laravel install, ready for you to develop.
