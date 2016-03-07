## Basic Commands

**Test start**

When you restart the Nginx service in command line on an Ubuntu server, the service crashes when a Nginx config file has errors. On a multi-site server this puts down all the sites, even the ones without config errors. To prevent this, I run the nginx config test first:
```
sudo nginx -t
```
