## Basic Authentication
To get a basic authentication for one of the folders (and its subfolders) on server include the following .htaccess file to that directory:
#### .htaccess
```
AuthUserFile "/absolute-path-to-your-pass-file/.htpasswd"
AuthName "Restricted Access"
AuthType Basic
Require valid-user
```
#### .htaccess
```
test:WIXKfQnanbUbL
```
