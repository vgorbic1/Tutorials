## Post Metadata
In WordPress, posts can have additional information attached to them. This information is called
post metadata and is saved in the `$wpdb->postmeta` table in the database. Post metadata is often referred to as Custom Fields 
in WordPress terminology.

### Adding Post Metadata
Use the `add_post_meta()` function to add new post metadata to a specific post, which accepts
four parameters.
```php
add_post_meta( $post_id, $meta_key, $meta_value, $unique );
```
- `$post_id` — The ID of the post to add metadata to.
- `$meta_key` — The metadata key (name) to add meta value(s) to.
- `$meta_value` — The value attributed to the meta key. Multiple meta values may be added
to a single key.
- `$unique` — Whether the meta value provided should be the only meta value. If true, there
will be only a single meta value. If false, multiple meta values can be added. By default,
this parameter is set to false.

To hide meta keys from appearing in the Custom Fields select box on the post -
editing screen, prefix the meta key with an underscore like `_favorite_song`.
This makes sure users never see it and is common practice when creating custom
meta boxes.

### Retrieving Post Metadata
WordPress makes it easy to get post metadata for display or to use in other PHP functions. A good
place to use this functionality is within The Loop with `get_post_meta` function. The `get_post_meta()`
function retrieves metadata for a specific post and accepts three parameters.
```php
get_post_meta( $post_id, $meta_key, $single );
```
- `$post_id` — The ID of the post to get the metadata for.
- `$meta_key` — The meta key name to retrieve meta value(s) for.
- `$single` — Whether to return a single meta value (true) or return an array of values
(false). By default, this parameter is set to false.

### Updating Post Metadata
The `update_post_meta()` function exists to update previous metadata for a specific post or to add
new metadata if it is not already set. This function accepts four parameters.
```php
update_post_meta( $post_id, $meta_key, $meta_value, $prev_value );
```
- `$post_id` — The post ID to update meta value(s) for.
- `$meta_key` — The meta key to update meta value(s) for.
- `$meta_value` — The new meta value to add to the meta key.
- `$prev_value` — The previous meta value to overwrite. If this parameter is not set, all meta
values will be overwritten in favor of the `$meta_value` parameter.

### Deleting Post Metadata
The `delete_post_meta()` function enables you to delete metadata for a specifi c post, and it accepts
three parameters.
```php
delete_post_meta( $post_id, $meta_key, $meta_value );
```
- `$post_id` — The post ID to delete metadata for.
- `$meta_key` — The meta key to delete or the meta key to delete a meta value for.
- `$meta_value` — The meta value to delete for the given meta key. If this parameter is not set,
all meta values for the meta key will be deleted. If you want to delete
all the meta values for the favorite_song meta key for this post, leave the `$meta_value` parameter
empty.

