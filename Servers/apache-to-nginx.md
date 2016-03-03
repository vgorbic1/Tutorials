## Migrate from an Apache Web Server to Nginx on an Ubuntu VPS
For many websites, a migration to Nginx would improve performance.

#### Install Nginx
Nginx is present in the Ubuntu repositories by default. Let's install it now:
```
sudo apt-get update
sudo apt-get install nginx
```
Nginx offloads any dynamic handling to a separate process. This allows Nginx to remain lean and fast. It can focus on its core functionality without having to try to add PHP support through modules. Instead, it just offloads that to an application that is built for that purpose. We need to install a PHP handler in order to process PHP scripts. The standard choice is php5-fpm, which performs well with Nginx:
```
sudo apt-get install php5-fpm
```

#### Set Up Test Nginx Configuration
Test Nginx on an alternative port until we are ready to solidify our changes. This way, we can run the two servers (Apache and Nginx) concurrently. Begin by opening the configuration file for the default Nginx site:
```
sudo nano /etc/nginx/sites-available/default
```
In the server { section, add a listen directive to tell Nginx to listen on a port other than port 80 (which Apache is still using to serve requests). For our tutorial, we'll use port 8000:
```
server {
    listen 8000;
    . . .
```
Save and close the file. This is a good time to do a spot check to see that we can access our Nginx server. Start Nginx to test this:
```
sudo service nginx start
```
Use the port number we configured to access the default Nginx configuration. Type this into your browser:
```
http://your_ip_or_domain:8000
```
Your Apache instance should still be running on the default port 80. 

#### Translate Your Apache Configuration
Begin migrating and translating your Apache configuration for use with Nginx. This task will mainly come down to writing Nginx server blocks, which are analogous to Apache virtual servers. Apache keeps these files in `/etc/apache2/sites-available/` and Nginx follow suit and keeps its server block declarations in `/etc/nginx/sites-available/` on Ubuntu. For each virtual server declaration, you'll be creating a server block. If you go through your Apache files, you will probably find virtual hosts that look like this:
```
<VirtualHost *:80>
    ServerAdmin webmaster@your_site.com
    ServerName your_site.com
    ServerAlias www.your_site.com

    DocumentRoot /var/www

    <Directory />
        Options FollowSymLinks
        AllowOverride None
    </Directory>

    <Directory /var/www/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        Order allow,deny
        allow from all
    </Directory>

    ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
    <Directory "/usr/lib/cgi-bin">
        AllowOverride None
        Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
        Order allow,deny
        Allow from all
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    Alias /doc/ "/usr/share/doc/"
    <Directory "/usr/share/doc/">
        Options Indexes MultiViews FollowSymLinks
        AllowOverride None
        Order deny,allow
        Deny from all
        Allow from 127.0.0.0/255.0.0.0 ::1/128
    </Directory>
</VirtualHost>
```
We can begin to build our Nginx server block using this configuration. In your `/etc/nginx/sites-available/` directory, open the file we edited before to declare the Nginx port:
```
sudo nano /etc/nginx/sites-available/default
```
Disregarding the commented lines for the moment, it should look something like this:
```
server {
    listen 8000;

    root /usr/share/nginx/www;
    index index.html index.htm;

    server_name localhost;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /doc/ {
        alias /usr/share/doc/;
        autoindex on;
        allow 127.0.0.1;
        deny all;
    }
}
```
The main directives translate like this:
```
Apache                                 Nginx
------                                 ------

<VirtualHost *:80>                     server {
                                            listen 80;

ServerName yoursite.com
ServerAlias www.yoursite.com           server_name yoursite.com www.yoursite.com;

DocumentRoot /path/to/root             root /path/to/root;

AllowOverride All                      (No Available Alternative)

DirectoryIndex index.php               index index.php;

ErrorLog /path/to/log                  error_log /path/to/log error;

CustomLog /path/to/log combined        access_log /path/to/log main;

Alias /url/ "/path/to/files"           location /url/ {
<Directory "/path/to/files">                 alias /path/to/files;
```
If we were going to create a server block that emulates the functionality of the virtual host file from above, it might look something like this:
```
server {
    listen 8000;   # We're deliberately leaving this as-is to avoid conflict at the moment

    root /var/www;
    server_name your_site.com www.your_site.com;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }

    location /doc/ {
        alias /usr/share/doc/;
        autoindex on;
        allow 127.0.0.1;
        deny all;
    }

    location ~/\.ht {
        deny all;
    }

}
```
Firstly, the error log lines have been eliminated from the configuration. This is because they are already defined in the /etc/nginx/nginx.conf file. This provides us with a default that we will use.

We have also eliminated the ServerAdmin directive because Nginx does not embed that information in its error pages.

The PHP handling has changed a bit as well. Due to the fact that PHP is handled separately in Nginx, we pass these files off to the php-fpm program we installed earlier. This is implemented through a socket (which we will need to configure momentarily).

The documentation section is changed to reflect the Nginx documentation. It otherwise functions fairly similarly.

Lastly, we configure Nginx to deny access to any .htaccess or other files that begin with .ht in our directory. These are Apache-specific configuration files, and they do not work with Nginx. It is safer to not expose these configuration files.

Save and close the file when you are finished. We must restart our Nginx server for these changes to be recognized:
```
sudo service nginx restart
```
#### Configure PHP-FPM
Now that we have most of the Nginx configuration out of the way, we need to modify the php-fpm configuration to communicate using the channels we specified. To begin with, we should modify the php.ini file so that it doesn't serve files insecurely.
```
sudo nano /etc/php5/fpm/php.ini
```
The line that we need to modify will require PHP to serve the exact file requested instead of guessing if there is an incomplete match. This prevents PHP from possibly serving or exposing sensitive data to someone who is probing the PHP handler for weaknesses.
Find the line that specifies the `cgi.fix_pathinfo` directive and modify it so that it looks like: `cgi.fix_pathinfo=0` Save and exit out of this file.

Next, we will change the way that php-fpm connects to our server. Open this file in your editor:
```
sudo nano /etc/php5/fpm/pool.d/www.conf
```
Find and modify the `listen` directive to match the value that we put in the server block configuration file:
```
listen = /var/run/php5-fpm.sock
```
If you end up running into problems with handling a lot of PHP requests, you might want to come back here and increase the number of child processes that can be spawned at once. The line you want to change is:
```
pm.max_children = Num_of_children
```
Save and close this file.
Now, our php-fpm program should be configured correctly. We need to restart it for our changes to propagate.
```
sudo service php5-fpm restart
```
It won't hurt to restart Nginx again as well:
```
sudo service nginx restart
```
Test that any PHP files that you have in your root directory function correctly. You should be able to get PHP files to execute just as they were in Apache. If we access the `info.php` file that we created in the Ubuntu LAMP tutorial, it should render like this:
```
http://your_ip_or_domain:8000/info.php
```
In the PHP Variables section, you should see Nginx listed as the "SERVER_SOFTWARE" variable.

#### Transition Your Nginx Site Live
the only thing we need to do is modify the port in the Nginx server block. Open the file now:
```
sudo nano /etc/nginx/sites-available/default
```
Change the port back to the default port 80. This will allow it to start accepting regular HTTP traffic as soon as it is restarted.
```
server {
    # listen 8000;
    listen 80;
    . . .
```
Save and close the file.

If you're planning on continuing to run Apache, check these files and locations for port 80 usage:
```
/etc/apache2/ports.conf
/etc/apache2/apache2.conf
/etc/apache2/httpd.conf
/etc/apache2/sites-enabled/  ## Search all sites in this directory
```
After you are satisfied that you have changed all of the necessary ports, you can restart both services like this:
```
sudo service apache2 reload && sudo service nginx reload
```
Apache should reload, releasing port 80. Immediately afterward, Nginx should reload and start accepting connections on that port. If all went smoothly, your site should now be served by Nginx.

If you are not going to be using Apache anymore to serve any portion of your sites, you can completely stop its web process instead:
```
sudo service apache2 stop && sudo service nginx reload
```
If you are not using Apache anymore, you can uninstall the Apache files at this point. You can easily find the Apache-related files by typing:
```
dpkg --get-selections | grep apache
```
You can then uninstall them with apt-get. For example:
```
sudo apt-get remove apache2 apache2-mpm-prefork apache2-utils apache2.2-bin apache2.2-common libapache2-mod-auth-mysql libapache2-mod-php5
```
You can also remove all of the dependency packages that are no longer needed:
```
sudo apt-get autoremove
```

#### Migration Complications
**Rewrite Translations and .htaccess Files**

One of the most fundamental differences is that Nginx does not respect directory overrides.

Apache uses `.htaccess` files, together with an `AllowOverride All` directive in a location block. This allows you to put directory-specific configurations in the directory that houses the files.

Nginx does not allow these files. Housing the configuration with the files being served is potentially a security problem if misconfigured, and it is easy to look at the centralized configuration files and not realize that a setting is being overwritten through an `.htaccess` file.

As a result, all configuration that you have listed in an active `.htaccess` file must be placed within the location block in the server block configuration for that host. This is not generally any more complicated, but you must translate these rules just as you did with the virtual host definitions.

A common thing to keep in `.htaccess` files are rules for Apache's `mod_rewrite` module, which alters the access URLs of content to be more user-friendly. Nginx has a rewrite module that is similar, but uses different syntax. 

**Module and Outside Configuration Complications**

Another thing to keep in mind is that you need to be conscious of what functionality the Apache modules that you have enabled are providing. A simple example is the `dir` module. When enabled, you can specify the order of the files that Apache will attempt to serve as a directory index by placing a line like this in your virtual host file:
```
DirectoryIndex index.html index.htm
```
This line will determine the handling that will happen for this virtual host. However, if this line is not present, and the dir module is enabled, the order of files being served will be determined by this file:

sudo nano /etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>

          DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm

</IfModule>
The point of bringing this up is that you have to be aware of the possibility that a module, or an externally sourced configuration of any kind, for that matter, might be doing something behind-the-scenes that you will have to do explicitly in Nginx. In this example, you can specify the directory index order in Nginx by adding this to a server block:
```
server {
    . . .
    index index.php index.html index.htm;
    . . .
```
One thing that might be helpful if you are transitioning a complex site configuration is to copy and paste all of the separately sourced configuration files into one monolithic file and systematically go through and translate each line. This might be a headache, but for a production server, it could save you a lot of time tracking down what is causing strange behavior that you cannot quite pin down.
