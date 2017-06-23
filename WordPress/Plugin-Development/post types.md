## Post Types
You use the `register_post_type()` function to create new post types for a site.
```php
register_post_type( $post_type, $args );
```
The function returns the post type object and accepts two parameters:
- `$post_type` — The name of the post type. This should contain only alphanumeric
characters and underscores.
- `$args` — An array of arguments that define the post type and how it should be handled
within WordPress:
1. `public` handles whether the post type should be shown on the frontend of the
site and backend. By default, this is set to false. This is a catchall argument that defines the
`show_ui`, `publicly_queryable`, and `exclude_from_search` arguments if they are not set
individually.
2. `show_ui` controls whether administration screens should be shown for the post type in the admin.
This defaults to the value set by the public argument.
3. `publicy_queryable` controls whether the post type should be publicly queryable from the frontend
of the site. This defaults to the value set by the public argument.
4. `exclude_from_search` enables you to exclude your post type’s posts from search results on the site. By
default, this is set to the value of the public argument.
5. `supports` enables plugins to define what features their post types support. It accepts
an array of values that WordPress checks for internally. If your plugin does not set this argument, it
defaults to the title and editor arguments:
`title` — Enables users to enter a post title.
`editor` — Displays a content editor on the post editing screen with a media uploader.
`author` — Offers a select box to choose the author of the post.
`thumbnail` — Presents a featured image box for the post.
`excerpt` — Creates an excerpt editor on the post editing screen.
`comments` — Shows whether comments will be enabled for posts of this type.
`trackbacks` — Shows whether trackbacks and pingbacks will be enabled for posts of this type.
`custom-fields` — Shows the custom field editing area on the post edit screen.
`page-attributes` — Displays the attributes box for choosing the post order. The
hierarchical argument must be set to true for this to work.
`revisions` — Saves revisions of posts of this type.
6. `labels` is an array of text strings shown in various places in the admin for the post
type.
7. `capability_type` enables you to add a custom set of capabilities. It acts as a catchall term from which
new capabilities are created. The capabilities argument can overwrite individual capabilities set
by this argument. By default, its value is post.
8. `capabilities` is an array of custom capabilities required for editing, deleting,
reading, and publishing posts of this type.
9. `hierarchical` enables you to set the posts of this type to be ordered hierarchically
(such as the WordPress “page” post type) or nonhierarchically (such as the WordPress “post” post
type). If set to true, posts can be arranged in a hierarchical, tree - like structure. By default, the
argument is set to false.
10. `has_archive` creates an archive page for the post type, much like the WordPress
posts page that displays the site’s latest blog posts. How these posts are displayed is dependent
on the theme the user has installed. By default, this argument is set to false. If it is set to true,
WordPress will create the archive.
11. `query_var` is the name of the query variable for posts of this type. For example, you would use
this when querying posts of this type from the database.
12. `rewrite` creates unique permalinks for this post type. Valid values for it are true,
false, or an array. If set to true, it will create permalinks from the `query_var` argument and the
individual post title. If set to false, no permalink structure will be created.
If using an array, you may set several values:
`with_front` — Whether to prefi x permalinks with the permalink front base. By default,
this is set to true.
`slug` — A unique string to use before the post title in the permalink. This defaults to the
`query_var` argument.
`feeds` — Whether the post type should have feeds for its posts. The `has_archive` argument
needs to be set to true for this to take effect. Its value will default to the `has_archive` value
if neither is set.
`pages` — Whether post type archive pages should be paginated. By default, it is set to true.
This feature is only useful if the `has_archive argument` is also set to true.
13. `taxonomies`
This argument enables you to add support for preexisting taxonomies to the post type. It accepts an
array of taxonomy names as its value.
14. `menu_position` enables you to set the position in which the administration menu item shows in the
admin menu. By default, new post types are added after the Comments menu item.
15. `menu_icon` accepts an image filename to use as the menu icon in the admin menu.
16. `show_in_nav_menus` If you want to allow posts of this type to appear in WordPress nav menus, set this to true;
otherwise, set it to false. By default, it is set to the value of the public argument.
17. `can_export` WordPress has an import/export feature that enables users to import or export posts. This
argument enables you to set whether users can export posts of this type. It is set to true by default.
18. `register_meta_box_cb` Plugins can add meta boxes to the edit post screen. This argument enables plugins to set a custom
callback function for adding custom meta boxes within the `add_meta_box()` function for this post type.
19. `permalink_epmask`
This is the rewrite endpoint bitmask used for posts of this type. By default, this is set to `EP_PERMALINK`.

Sample plugin code:
```php
/*
Plugin Name: Music Collection Post Types
Plugin URI: http://example.com
Description: Creates the music_album post type.
Version: 0.1
Author: WROX
Author URI: http://wrox.com
*/
/* Set up the post types. */
add_action( 'init', 'boj_music_collection_register_post_types' );
/* Registers post types. */
function boj_music_collection_register_post_types() {
 /* Set up the arguments for the 'music_album' post type. */
 $album_args = array(
  'public' = > true,
  'query_var' = > 'music_album',
  'rewrite' = > array(
  'slug' = > 'music/albums',
  'with_front' = > false,
 ),
 'supports' = > array(
  'title',
  'thumbnail'
 ),
 'labels' = > array(
  'name' = > 'Albums',
  'singular_name' = > 'Album',
  'add_new' = > 'Add New Album',
  'add_new_item' = > 'Add New Album',
  'edit_item' = > 'Edit Album',
  'new_item' = > 'New Album',
  'view_item' = > 'View Album',
  'search_items' = > 'Search Albums',
  'not_found' = > 'No Albums Found',
  'not_found_in_trash' = > 'No Albums Found In Trash'
  ),
 );
 /* Register the music album post type. */
 register_post_type( 'music_album', $album_args );
}
```
