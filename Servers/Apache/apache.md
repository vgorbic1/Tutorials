## Apache

#### Commands
To start Apache running on Ubuntu:
```
sudo /etc/init.d/apache2 restart
sudo /etc/init.d/apache2 start
sudo /etc/init.d/apache2 stop
```
To check status:
```
sudo /etc/init.d/apache2 status
```
To get version number:
```
/usr/sbin/apache2 -v
```

To check configuration files:
```
sudo apache2 -t
```

#### Apache Folders:
- /etc/apache2/ contains apache2.conf
- /etc/init.d/ contains system startup/shutdown scripts
- /var/www/ default server icons, CGI and HTML files
- /usr/share/ apache documentation
- /usr/sbin/ executable files
- /usr/bin/ some utilities here
- /var/log/apache2/ log files
