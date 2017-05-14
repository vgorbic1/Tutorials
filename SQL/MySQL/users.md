## Basic User Commands

### Log in MySQL
Login as root in MySQL using the following command:
```
mysql -u root -p
```
If it is a fresh MySQL installation, the root user will have empty password.

### Uses and Permissions
Select all MySQL users, their corresponding host and password:
```sql
SELECT User, Host, Password FROM mysql.user;
```
To create a new user and grant custom permissions:
```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```
The user has no permissions to do anything yet, and would not even log into the shell.

To grant all privileges to the new user. this specific command allows to the user to read, edit, execute 
and perform all tasks across all the databases and tables:
```sql
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
```
To make all changes be in effect:
```sql
FLUSH PRIVILEGES;
```
To grant custom privileges use this template:
```
GRANT [type of permission] ON [database name].[table name] TO '[username]'@'localhost';
```
- ALL PRIVILEGES allows a MySQL user all access to a designated database (or if no database is selected, across the system)
- CREATE allows them to create new tables or databases
- DROP allows them to them to delete tables or databases
- DELETE allows them to delete rows from tables
- INSERT allows them to insert rows into tables
- SELECT allows them to use the Select command to read through databases
- UPDATE allow them to update table rows
- GRANT OPTION allows them to grant or remove other users' privileges

Do not forget to flush the privileges.

To revoke permissions use this template
```
 REVOKE [type of permission] ON [database name].[table name] FROM '[username]'@'localhost';
```
Do delete a user:
```
DROP USER 'username'@'localhost';
```

