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
