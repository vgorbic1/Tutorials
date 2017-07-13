## Configuration
The core settings of your Laravel application—database connection, queue and mail
settings, etc.—live in files in the config folder. Each of these files returns an array, and
each value in the array will be accessible by a config key that is comprised of the filename
and all descendant keys, separated by dots (.)
So, if you create a file at `config/services.php` that looks like this:
```
// config/services.php
return [
 'sparkpost' => ['secret' => 'abcdefg']
];
```
you will now have access to that config variable using `config('services.spark
post.secret')`.

Any configuration variables that should be distinct for each environment (and therefore
not committed to source control) will instead live in your `.env` files. Let’s say you
want to use a different Bugsnag API key for each environment. You’d set the config
file to pull it from `.env`:
```
// config/services.php
return [
 'bugsnag' => ['api_key' => env('BUGSNAG_API_KEY')]
];
```
This `env()` helper function pulls a value from your `.env` file with that same key. So
now, add that key to your `.env` (settings for this environment) and `.env.example` (template
for all environments) files:
```
BUGSNAG_API_KEY=oinfp9813410942
```
Your `.env` file already contains quite a few environment-specific variables needed by
the framework, like which mail driver you’ll be using and what your basic database
settings are.
