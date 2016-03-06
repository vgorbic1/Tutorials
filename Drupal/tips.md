## Some useful tips

- It is a best practice to avoid creating site content with user/1. That is so because it is awkward when responsibility for site maintenance done as User/1 needs to change to a new person if the original User/1 wrote content that still needs to be associated with him/her. The content written by the original author would have to then be assigned to a new user account. It's better to simply create that second account immediately after installing the site.
- User/0 or Anonymous user: User/0 is reserved for the unregistered/anonymous user. In database 'users' table uid = 0 is assigned for anonymous users. Note: Database users table uid = 0 row must exist or the site will have severe problems.
- `include_once()` and `require_once()` are statements, not functions. You don't need parentheses around the file name to be included.
- When including code from the same directory or a sub-directory, start the file path with ".":
`include_once ./includes/mymodule_formatting.inc`
In Drupal 7.x and later versions, use `DRUPAL_ROOT`:
`require_once DRUPAL_ROOT . '/' . variable_get('cache_inc', 'includes/cache.inc');`
