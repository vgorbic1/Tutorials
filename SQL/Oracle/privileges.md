## Privileges

SQL privileges provide System Security and Data Security.
DBA is a high-level user who can create users and grant users access to the database and its objects.
Schema is owned by a database user and has the same name as the user.
DBA can create a user:
```
CREATE USER username IDENTIFIED BY password;
```
Username may have 30 characters by default and have _, $, or #.
To set a temporary password (user can change it when first time logged in) use:
```
CREATE USER username IDENTIFIED BY password PASSWORD EXPIRE;
```
Now, DBA can grant some minimum privileges to the user, so the user can have access to the database.

#### SYSTEM PRIVILEGES
System privileges allow access to perform DDL operations, such as CREATE, ALTER and DROP on database objects. Almost 200 privileges are available. To see all system privileges go to SYSTEM_PRIVILEGE_MAP.
```
GRANT CREATE SESSION TO username; - allow user to connect to the database
GRANT ALL;
```

#### OBJECT PRIVRLEGES
Object privileges allow performing DML operations, such as INSERT and UPDATE on the data in database.
Thus UPDATE will be an object privilege.
```
GRANT SLECT, INSERT ON scott.customers TO thomas WITH GRANT OPTION;
```
WITH GRANT OPTION is used only for users, but not for roles!
```
GRANT update (department_name, location_id) ON departments TO demo, manager;
REVOKE SELECT, INSERT ON departments FROM demo;
REVOKE ALL ON departments FROM demo;
```

#### Roles
A role is a named group of related privileges that can be granted to the user. User can have several roles. Oracle has several predefined roles for DBAs.
```
CREATE ROLE rolename;
GRANT create table, create view TO rolename;
GRANT rolename TO username, anotherusername;
```
- ALTER USER username DEFAULT ROLE rolename; - assign a default role.
- SET ROLE rolename; - to change the role that is currently enabled for a user.
- ALTER ROLE rolename IDENTIFIED BY password;  - add a password to the role.
- REVOKE rolename FROM username;
- DROP ROLE rolename; -users that had this role have to be reassigned with new privileges.

#### Changing password
A user can change its password:
```
ALTER USER username IDENTIFIED BY newpassword;
```

#### Removing user
```
DROP USER username;
```
To eliminate all objects in user’s schema so that the user can be deleted:
```
DROP USER username CASCADE;   
```
SESSION_PRIVS – a viewthat shows privileges active for the current user that haven’t been assigned via a role.
