## MySQL installation
To install MySQL in your Ubuntu box:
```
sudo apt-get install mysql-server
```
To install MySQL in your Centos box:
```
sudo yum install mysql-server
/etc/init.d/mysqld start
```
To access MySQL shell after installation:
```
mysql -u root -p
```
All MySQL commands end with a semicolon; if the phrase does not end with a semicolon, the command will not execute.

Although it is not required, MySQL commands are written in uppercase and databases, tables, usernames, or text are in 
lowercase to make them easier to distinguish. However, the MySQL command line is not case sensitive.

