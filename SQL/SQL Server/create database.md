## Microsoft SQL Server
### Create a Database on SQL Server
```sql
--create where
USE master;  
GO
--check if exists
IF DB_ID (N'MyDatabaseTest') IS NULL  
DROP DATABASE MyOptionsTest;  
GO 
--create database 
CREATE DATABASE MyDatabaseTest  
COLLATE SQL_Latin1_General_CP1_CI_AS  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO 
```
**GO signals the end of a batch of Transact-SQL statements to the SQL Server utilities.**
