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
Nginx does not care about files but rather locations and this is why we have a `try_files` directive inside the php block. This location block matches a URI that ends in .php but it does not care if it’s a file or not. Therefore a request for `/forum/avatars/user2.jpg/index.php` will be matched and sent to PHP, and if PHP is not configured properly PHP will then execute /forum/avatars/user2.jpg when /forum/avatars/user2.jpg/index.php doesn’t exist. This provides a huge security risk. Do note that this is not a bug in nginx, it’s the intended behaviour and as such will not be “fixed”.
