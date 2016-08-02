## SQL

#### Major Parts of SQL
- Data definition language (DDL) creates a database and all its structural componetns, tables, views, schemas. Modifies the structure of a database.
- Data manipulation language (DML) operates on the data content in the database.
- Data control language (DCL) mantains a database security and reliability.

#### Database Hierarchy
- DATABASE
- Catalog
- Schema (includes tables and related views if you want to keep one set of tables separate from the others)
- Table
- Atriburte

#### SQL Books:
If you’re an SQL veteran and you want to know more about optimization and how SQL is executed, get a copy of the excellent book SQL Tuning, by Dan Tow (Tow,
2003). For a look at the practical side of SQL through the lens of how not to use SQL, SQL Antipatterns: Avoiding the Pitfalls of Database Programming (Karwin, 2010) is a good
resource.

#### Tips
- It’s common to keep address information in the USERS table, in individual columns.
-You usually define the USERS table as follows:
```sql
create table USERS (
USERID int(11) not null primary key,
USERNAME varchar(15) not null,
ADDRESS_STREET varchar(255) not null,
ADDRESS_ZIPCODE varchar(5) not null,
ADDRESS_CITY varchar(255) not null
);
```

A **surrogate key** column is a primary key column with no meaning to the application user. Its only purpose is identifying data inside the application.

**Lazy loading** is retrieving data on demand only.
