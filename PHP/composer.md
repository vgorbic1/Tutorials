## Composer

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you. Composer is not a package (library) manager in the same sense as Yum or Apt are. It manages packages on a per-project basis, installing them in a directory inside your project. By default, it will never install anything globally. Thus, it is a dependency manager.

Suppose you have a project that depends on a number of libraries. Some of those libraries depend on other libraries. Composer enables you to declare the libraries you depend on, finds out which versions of which packages can and need to be installed, and downloads them into your project.

Composer is multi-platform and we strive to make it run equally well on Windows, Linux and OSX.

To update installed composer:
```
composer self-update
```

#### PROJECT SETUP
To start using Composer in your project, all you need is a composer.json file inside your project folder. This file describes the dependencies of your project and may contain other metadata as well. Tell Composer which packages your project depends on:
```
{
    "require": {
        "monolog/monolog": "1.0.*"
    }
}
```
The package name (in our case "monolog/monolog" ) consists of a vendor name and the project's name. Often these will be identical - the vendor name just exists to prevent naming clashes. Next, we are requiring version 1.0.* of Monolog. This means any version in the 1.0 development branch. By default, only stable releases are taken into consideration. 

#### INSTALLING DEPENDENCIES
To install the defined dependencies for your project, just run the install command from the folder where you put your composer.jason file:
```
composer install --no-dev
```

#### PACKAGIST
Packagist (packagist.org) is the main Composer repository. A Composer repository is a package source: a place where you can get packages from. Packagist aims to be the central repository that everybody uses. This means that you can automatically require any package that is available there.

#### AUTOLOADING
For libraries that specify autoload information, Composer generates a vendor/autoload.php file. You can simply include this file and you will get autoloading:
```php
require __DIR__ . '/vendor/autoload.php';
```
or simply:
```php
require_once 'vendor/autoload.php'
```
This makes it easy to use third party code. For example, if your project depends on Monolog, you can just start using classes from it, and they will be autoloaded:
```php
$log = new Monolog\Logger('name');
$log->pushHandler(new Monolog\Handler\StreamHandler('app.log',
    Monolog\Logger::WARNING));
$log->addWarning('Foo');
```
