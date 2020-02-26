## Nginx Installation
Install Nginx on CentOS 7
### Update the system
*-y* is an optional parameter. It serves to avoid confirmation questions. 
```
yum -y update
```

### Install Extra Packages
NGINX is not available in the standard repositories that come with the CentOS 
package, so you will need to install the EPEL repository on your server. This 
will ensure that you always have the latest version of NGINX. EPEL is free to 
use and provides numerous open-source packages to install with Yum.
```
yum install – y epel-release
```

### Install NGINX
```
yum –y install nginx
```

### Disable Apache and Start NGINX
Your instance of NGINX is installed, but it won’t start automatically. If you
already have an Apache server running, you will need to disable it before 
starting NGINX.
```
service httpd stop
```
Disable automatic starts by running the following command:
```
systemctl disable httpd
```
To start NGINX, run:
```
systemctl start nginx
```
To check its status, run:
```
systemctl status nginx
```
There should be a green piece of text that reads ‘active (running).’

### NGINX – Automatic Start Upon Boot
Most admins will want to make sure that NGINX starts up automatically 
whenever the server restarts:
```
systemctl enable nginx
```
### Set up Your Firewall to Allow Traffic
CentOS 7 enables firewalls by default and blocks access to ports 80 and 443. 
It will block any inbound HTTPS and HTTP packets from NGINX. To allow HTTP 
and HTTPS traffic:
```
firewall-cmd --zone=public --permanent --add-service=http

firewall-cmd --zone=public --permanent --add-service=https

firewall-cmd --reload
```
Done!

[MORE](https://phoenixnap.com/kb/how-to-install-nginx-on-centos-7)
