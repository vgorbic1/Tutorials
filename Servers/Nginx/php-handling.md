## Handling PHP
PHP ties in well with locations, namely we can define a location block to catch all PHP files. 
```
server {
    listen          80;
    server_name     forum.domain.com;
 
    index           index.php;
    root            /home/domain.com/forum;
 
    location ~* \.php$ {
        include fastcgi.conf # I include this in http context, it's just here to show it's required for fastcgi!
        try_files $uri =404; # This is not needed if you have cgi.fix_pathinfo = 0 in php.ini (you should!)
        fastcgi_pass 127.0.0.1:9000;
    }
}
```
Nginx does not care about files but rather locations and this is why we have a `try_files` directive inside the php block. This location block matches a URI that ends in .php but it does not care if it’s a file or not. Therefore a request for `/forum/avatars/user2.jpg/index.php` will be matched and sent to PHP, and if PHP is not configured properly PHP will then execute /forum/avatars/user2.jpg when /forum/avatars/user2.jpg/index.php doesn’t exist. This provides a huge security risk. Do note that this is not a bug in nginx, it’s the intended behaviour and as such will not be “fixed”. This can also be fixed on the PHP side by setting cgi.fix_pathinfo=0 in the php.ini file. The end result, though, is that .php files which exist will be passed via fastcgi to our PHP processes running on port 9000.

#### Search Engine Friendly URLs
Usually this involves quite a few rewrites, but with nginx we can do it with just one line, provided the backend script is written in a sane way.
```
server {
    listen          80;
    server_name     forum.domain.com;
 
    index           index.php;
    root            /home/domain.com/forum;
 
    location / {
        try_files   $uri $uri/ /index.php;
    }
 
    location ~* \.php$ {
        include fastcgi.conf; # I include this in http context, it's just here to show it's required for fastcgi!
        try_files $uri =404; # This is not needed if you have cgi.fix_pathinfo = 0 in php.ini (you should!)
        fastcgi_pass 127.0.0.1:9000;
    }
}
```
The one try files line means that it will first try accessing the full URI, which means that a static file request will end here. Secondly it will try the full URI plus a slash, thus looking for a directory. Finally, if none of these are found it will send the request to /index.php and perform a new location match, which will of course hit our PHP location and fastcgi_pass the request. PHP will then have the full URI in $_SERVER[‘REQUEST_URI’]. Simple, elegant and easy to understand.

#### URL with Parameters
```
location / {
   # try_files $uri $uri/ /index.php;
   try_files $uri $uri/ /index.php$is_args$args;
}
```
