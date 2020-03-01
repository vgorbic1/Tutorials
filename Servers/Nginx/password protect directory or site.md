## Password protect a directory

To password protect a directory called secret_folder, use the following directives inside the server 
block in the configuration file for your website.
```
location ^~ /secret_folder/ {
  auth_basic            "Restricted Area";
  auth_basic_user_file  conf/htpasswd;
}
```
This will password protect the directory, it’s sub folders and the files inside it. Change auth_basic_user_file 
directive to point to your htpasswd file. If your are using nginx version 0.6.7 or higher, note that the 
filename path is relative to directory of nginx configuration file, nginx.conf, rather than nginx prefix directory. 
So, if your nginx.conf is in /etc/nginx folder, the above code will use the htpasswd file in /etc/nginx/conf folder.

Here’s the format of the htpasswd file :
```
user:pass
user2:pass2:comment
user3:pass3
```
Passwords must be encoded by the crypt(3) function if Apache is not installed. If Apache is installed, you can 
use the htpasswd program to generate the htpasswd file:
```
htpasswd -b htpasswd NewUser NewPassword
```
If you want to use a web based utility to generate your htpasswd file, I’d recommend the excellent [.htaccess 
Password Generator](http://www.tools.dynamicdrive.com/password/) utility from Dynamic Drive.

### Password protect a site

In order to password protect the whole site, use the same code within location / block.
```
location / {
........................................
........................................
auth_basic            "Restricted Area";
auth_basic_user_file  conf/htpasswd;
}
```
