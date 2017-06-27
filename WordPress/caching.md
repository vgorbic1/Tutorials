## Caching
Caching is a way to store data for later use. People use many different types of caching and different
methods to cache data on their sites. You would typically save data that’s expensive to generate so
that it can be loaded quickly whenever it’s needed.

WordPress provides a method for plugins to handle caching. WordPress has the WordPress Object Cache feature, which
is a PHP class that plugins can use for storing data. WordPress doesn’t store this data on its own.
It provides a way for caching plugins to cache the data.

Two great benefi ts exist for using WordPress’ built-in method for caching.
- There’s a single set of functions that all plugins can use without conflicting with other
plugins.
- Caching plugins can be created to handle persistent caching, which saves data across
multiple page views.

The `wp_cache_add()` function should be used when your plugin needs to store data to a cache key
that doesn’t already exist. If the cache key does exist, no data will be added.
```php
wp_cache_add( $key, $data, $group, $expire );
```
The `wp_cache_replace()` function enables plugins to overwrite previously saved data for the cache key.
```php
wp_cache_replace( $key, $data, $group, $expire );
```
The `wp_cache_set()` function is a combination of the `wp_cache_add()` and `wp_cache_replace()`
function. If the data for the cache key is not already saved, it will create it. If it does exist, it will
overwrite the preexisting data.
```php
wp_cache_set( $key, $data, $group, $expire );
```
The `wp_cache_get()` function provides a way for plugins to load cached data by cache key and
group. It returns false if no data is found. It returns the cached data if it exists.
```php
wp_cache_get( $key, $group );
```
The `wp_cache_delete()` function clears cached data for the specified cache key and group. It
returns true if the data was successfully removed and false if not.
```php
wp_cache_delete( $key, $group );
```

- `$key` — A unique ID to store and retrieve data by. The cache key doesn’t need to be unique
across multiple cache groups, but it must be unique within an individual group.
- `$data` — The data your plugin wants to save and retrieve.
- `$group` — A way to group multiple pieces of cached data. For example, multiple cache keys
can be grouped together. This parameter is optional.
- `$expire` — How long the data should be stored in seconds. This parameter is optional and
defaults to 0, allowing the data to be stored indefinitely.
