## SQL

#### SQL Books:
If you’re an SQL veteran and you want to know more about optimization and how SQL is executed, get a copy of the excellent book SQL Tuning, by Dan Tow (Tow,
2003). For a look at the practical side of SQL through the lens of how not to use SQL, SQL Antipatterns: Avoiding the Pitfalls of Database Programming (Karwin, 2010) is a good
resource.

#### Tips
- It’s common to keep address information in the USERS table, in individual columns.
-You usually define the USERS table as follows:
```sql
create table USERS (
USERNAME varchar(15) not null primary key,
ADDRESS_STREET varchar(255) not null,
ADDRESS_ZIPCODE varchar(5) not null,
ADDRESS_CITY varchar(255) not null
);
```
