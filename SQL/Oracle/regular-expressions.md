## REGULAR EXPRESSIONS
Regular expressions enable you to implement complex match logic in the database with the following benefits:
- By centralizing match logic in Oracle Database, you avoid intensive string processing of SQL results sets by middle-tier applications.
- Using server-side regular expressions to enforce constraints, you eliminate the need to code data validation
logic on the client.
- The built-in SQL and PL/SQL regular expression functions and conditions make string manipulations more powerful
and easier than in previous releases of Oracle Database 10g.

#### REGEXP_LIKE
Is similar to the LIKE operator, but performs regular expression matching instead of simple pattern matching. 

Example:
```
SELECT first_name, last_name
FROM employees
WHERE REGEXP_LIKE (first_name, '^Ste(v|ph)en$');
```

#### REGEXP_SUBSTR 
```
Searches for a regular expression pattern within a given string and extracts the matched substring.

Example:
```
SELECT REGEXP_SUBSTR(street_address , ' [^ ]+ ') AS Road
FROM locations;
```

#### REGEXP_COUNT
Returns the number of times a pattern match is found in an input sting.

Example:
```
SELECT REGEXP_COUNT(
'ccacctttccctccactcctcacgttctcacctgtaaagcgtccctccctcatccccatgcccccttaccctgcag
ggtagagtaggctagaaaccagagagctccaagctccatctgtggagagg', 'gtc') AS Count
FROM dual;
```

#### REGEXP_INSTR 
Searches a string for a regular expression pattern and returns the position where the match is found.

Example:

```
SELECT street_address,
REGEXP_INSTR(street_address,'[[:alpha:]]') AS First_Alpha_Position
FROM locations;
```

#### REGEXP_REPLACE
Searches for a regular expression pattern and replaces it with a replacement string.

Example:
```
SELECT REGEXP_REPLACE(phone_number, ‘\.',‘-') AS phone
FROM employees;
```

#### Regular Expressions and Check Constraints
```
ALTER TABLE emp8
  ADD CONSTRAINT email_addr
  CHECK(REGEXP_LIKE(email,'@')) NOVALIDATE;
```
The following statement will return an error since the email address is not matching the regular expression in the check constraint:
```
INSERT INTO emp8 VALUES
(500,'Christian','Patel','ChrisP2creme.com',
1234567890,'12-Jan-2004','HR_REP',2000,null,102,40);
```
