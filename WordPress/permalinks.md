## Permalinks and Rewriting API
### Apache's mod_rewrite
The key module for permalinks in Apache is `mod_rewrite`, a module that enables defining rewrite
rules typically found in the `.htaccess` file. A classic rewrite rule consists in the following code block:
```
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteRule [ pattern] [ substitution ] [ optional flag(s) ]
</IfModule>
```
The pattern and substitution parameters can use regular expressions. Consider for instance the
following rewrite rule:
```
RewriteRule /buy/([^/]+)/ /shop.php?product=$1 [L]
```
When installed, WordPress creates an `.htaccess` file in its root directory that contains the
following block:
```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
```
1. If the request is index.php, redirect to this file and don’t try to match any other rewrite
rule. (The [L] flag stands for Last.)
2. If the request is not a file ( %{REQUEST_FILENAME} ! - f ) ...
3. ... and if the request is not a directory ( %{REQUEST_FILENAME} ! - d ) ...
4. ... then rewrite the URL to index.php and don’t try to apply another rewrite rule.

This means that
practically all requests in the frontend area of a WordPress site are internally redirected to index
.php , which then has to guess how to interpret the request.

### Overview of the Query Process
1. The root `index.php` file is loaded, as per the `.htaccess` rewrite rule, and loads the file
`wp-blog-header.php`.
2. This file loads `wp-load.php`, which searches and includes `wp-config.php`, which will
in turn load `wp-settings.php` that includes the function files, active plugins, and then
pluggable functions.
3. Two new objects are instantiated: `$wp_query` and `$wp_rewrite`.
4. A few other files are loaded, such as translation files and the theme’s functions file.
WordPress is now fully loaded and plugins can start interacting, but it doesn’t know yet
what to display and what page has been requested. Back to `wp-blog-header.php`: After
everything is loaded, this file calls the function `wp()` , which starts the magic — the function
`WP::parse_request()`. The function `parse_request()` from the WP class (found in `wp-includes/classes.php` ) prepares
everything WordPress needs to know to understand the page request:
5. This function fetches the list of all the registered rewrite rules. Just as previously explained
with `mod_rewrite`, it consists in a list of *pattern => replacement* pairs, to tell WordPress
that */category/tutorials/page/2/* actually means */index.php?category_name
=tutorials&paged=2*.
6. The function goes through each rewrite rule, compares it to the requested URL, and tries to
find a match. If no match is eventually found, this is a 404 error. 
At this point, if the page is not a 404 error, WordPress now has a permalink translation pattern
with query variable placeholders, such as *index.php?category_name=[string]&paged=[number]*.
It now needs to get the values of these query variables.
7. The function `parse_request()` now obtains the list of the registered query variables, and
for each variable checks if a value has been set by the permalink pattern, by POST, or by
GET submission.
8. Now, WordPress knows everything it needs to convert the initial URL request into a proper
MySQL database query, get post data, load the required theme template, and display the
requested page.


