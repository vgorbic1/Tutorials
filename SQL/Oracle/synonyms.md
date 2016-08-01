## SYNONYMS
A synonym is an alternative name for objects such as tables, views, sequences, stored procedures, and other database objects. You generally use synonyms when you are granting access to an object from another schema and you don't want the users to have to worry about knowing which schema owns the object. The object cannot be in a package, though.

#### CREATE SYNONYM
Creates a synonym.

Syntax:
```
CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema .] synonym_name
  FOR [schema .] object_name [@ dblink];
```
Example:
```
CREATE PUBLIC SYNONYM suppliers
FOR app.suppliers;
```
Now Instead of writing SELECT * FROM app.suppliers; write SELECT * FROM suppliers;

#### DROP SYNONYM
Drops the synonym. Only the database admin can drop a public synonym.

Syntax:
```
DROP [PUBLIC] SYNONYM [schema .] synonym_name [FORCE];
```
- PUBLIC allows you to drop a public synonym. If you have specified PUBLIC, then you don't specify a schema.
- FORCE will force Oracle to drop the synonym even if it has dependencies. It is probably not a good idea to use force as it can cause invalidation of Oracle objects.

Example:
```
DROP PUBLIC SYNONYM suppliers;
```
Check information on synonyms in the USER_SYNONYMS view.
