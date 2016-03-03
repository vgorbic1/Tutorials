## How To Migrate from an Apache Web Server to Nginx on an Ubuntu VPS
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
