## Form-based Authentication/Authorization

Consider that you have a website that contains some pages/resources that anyone should be able to access, 
and some pages/resources that only certain types of users should be able to access. To accomplish this, we will 
focus on the simplest, yet convenient, method of authorization: FORM-based authorization provided by Tomcat. 
We will use the `server.xml` and `web.xml` files, a `j_security_check` form (for FORM-based) in a JSP page that requires 
two parameters `j_username` and `j_password`, and will specify roles (groups) within our MySQL database.

#### Create tables in your application's database to hold user and role information
```sql
create table users (
user_name         varchar(15) not null primary key,
user_pass         varchar(15) not null
);

create table user_roles (
user_name         varchar(15) not null,
role_name         varchar(15) not null,
primary key (user_name, role_name)
);

// Create a user so that Tomcat can access the database you just created.
CREATE USER 'tomcat'@'localhost' IDENTIFIED BY 'tomcat';

// Give the tomcat user privileges to read.
GRANT SELECT ON sample.* TO 'tomcat'@'localhost';

// Create some users:
insert into users values ('admin', 'admin');

// Add some roles:
insert into user_roles values ('admin', 'administrator');
```

#### Set up Tomcat to use JDBCRealm and your newly created tables.
Example Realm elements are included (commented out) in the default $CATALINA_BASE/conf/server.xml file. 
Here's an example for using a MySQL database called "sample", configured with the tables described above, 
and accessed with username "tomcat" and password "tomcat":
```xml
<Realm className="org.apache.catalina.realm.JDBCRealm"
    driverName="com.mysql.jdbc.Driver"
    connectionURL="jdbc:mysql://localhost:3306/sample?user=tomcat&amp;password=tomcat"
    userTable="users" userNameCol="user_name" userCredCol="user_pass"
    userRoleTable="user_roles" roleNameCol="role_name"/>
```

#### Add login capability to your web application
Create the login page in your web application. The form action must be defined exactly as below. The input type and name for username and password must be defined exactly as below.
Other parts of the form can be of your own design.
```html
<FORM ACTION="j_security_check" METHOD="POST">
<TABLE>
<TR><TD>User name: <INPUT TYPE="TEXT" NAME="j_username"> 
<TR><TD>Password: <INPUT TYPE="PASSWORD" NAME="j_password"> 
<TR><TH><INPUT TYPE="SUBMIT" VALUE="Log In">
</TABLE>
</FORM>
```
Create the login error page in your web application. This page will be shown when login information is entered incorrectly. 
There are no restrictions on the design of this page.

Add configuration to the application web.xml, i.e., specify the login and error pages.
```xml
<!-- Tell the server to use form-based authentication. --> 
<login-config>
    <auth-method>FORM</auth-method> 
    <form-login-config>
        <form-login-page>/admin/login.jsp</form-login-page>
        <form-error-page>/admin/login-error.jsp</form-error-page> 
    </form-login-config>
</login-config>
```
#### Configure which resources require login in the web application
Specify which resources require login.
```xml
<!-- Protect everything within the "investing" directory. --> 
<security-constraint>
    <web-resource-collection> 
        <web-resource-name>investing</web-resource-name> 
        <url-pattern>/investing/*</url-pattern>
    </web-resource-collection> 
    <auth-constraint>
        <role-name>registered-user</role-name>
        <role-name>administrator</role-name> 
    </auth-constraint>
</security-constraint>
```
