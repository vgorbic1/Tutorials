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
