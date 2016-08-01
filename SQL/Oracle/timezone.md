## TIMEZONE
Greenwich Mean Time (GMT) now known as Coordinated Universal Time (UTC). It is also called  zero altitude and is not affected by summer time or daylight saving time. 

TIME_ZONE may be set to:

- ALTER SESSION SET TIME_ZONE = '-05:00';  (An absolute offset)
- ALTER SESSION SET TIME_ZONE = dbtimezone; Database time zone
- ALTER SESSION SET TIME_ZONE = local; OS local time zone
- ALTER SESSION SET TIME_ZONE = 'America/New_York'; A named region

Display the value of the database time zone:  SELECT DBTIMEZONE FROM DUAL;

Display the value of the session’s time zone:  SELECT SESSIONTIMEZONE FROM DUAL;

#### CURRENT_DATE
Returns the current date from the user session and has a data type of DATE.

#### CURRENT_TIMESTAMP
Returns the current date and time from the user session and has a data type of TIMESTAMP WITH TIME ZONE.

#### LOCALTIMESTAMP
Returns the current date and time from the user session and has a data type of TIMESTAMP.

#### TIMESTAMP
Extends the DATE datatype. It contains the year, month, any day values of date, hour, minute, and seconds.
```
CREATE TABLE web_orders(order_date TIMESTAMP WITH TIME ZONE,
    delivery_time TIMESTAMP WITH LOCAL TIME ZONE);
```

#### INTERVAL
Used to store the difference between two datetime values:

INTERVAL YEAR TO MONTH:
```
CREATE TABLE warranty
  (prod_id number, warranty_time INTERVAL YEAR(3) TO MONTH);
INSERT INTO warranty VALUES (123, INTERVAL '8' MONTH);
INSERT INTO warranty VALUES (155, INTERVAL '200' YEAR(3));
INSERT INTO warranty VALUES (678, '200-11');
```

INTERVAL DAY TO SECOND:
```
CREATE TABLE lab ( exp_id number, test_time INTERVAL DAY(2) TO SECOND);
INSERT INTO lab VALUES (100012, '90 00:00:00');
INSERT INTO lab VALUES (56098, INTERVAL '6 03:30:16' DAY TO SECOND);
```

#### FUNCTIONS
EXTRACT()

Extracts and returns the value specified datetime field from a datetime or interval value expression.
```
SELECT EXTRACT (YEAR FROM SYSDATE) FROM DUAL;
```
TZ_OFFSET()

Returns the time zone offset corresponding to the value entered.
```
SELECT TZ_OFFSET('US/Eastern') FROM DUAL;
```

FROM_TZ()

Converts a TIMESTAMP value to a TIMESTAMP WITH TIME ZONE value.
```
SELECT FROM_TZ(TIMESTAMP '2000-07-12 08:00:00', 'Australia/North') FROM DUAL;
```

TO_TIMESTAMP()

Converts a string of CHAR data type to a value of the TIMESTAMP data type.
```
SELECT TO_TIMESTAMP ('2007-03-06 11:00:00','YYYY-MM-DD HH:MI:SS') FROM DUAL;
```

TO_YMINTERVAL()

Converts a character string to an INTERVAL YEAR TO MONTH data type. Display a date that is one year and two months after the hire date: 
```
SELECT hire_date, hire_date + TO_YMINTERVAL('01-02') AS HIRE_DATE_YMININTERVAL
FROM employees;
```

TO_DSINTERVAL()
Display a date that is 100 days and 10 hours after the hire date for all the employees:
```
SELECT last_name,
  TO_CHAR(hire_date, 'mm-dd-yy:hh:mi:ss') AS hire_date,
  TO_CHAR(hire_date + TO_DSINTERVAL('100 10:00:00'),'mm-dd-yy:hh:mi:ss') 
  AS hiredate2 
FROM employees;
```

#### DAYLIGHT SAVING TIME
Most western nations advance the clock ahead one hour during the summer months. This period is called daylight saving time. It lasts from the first Sunday in April to the last Sunday in October in the US, Canada and Mexico. In Europe it starts one week earlier and ends the same time as in the US.
Oracle automatically jumps according to the time zone:

**First Sunday in April**
– Time jumps from 01:59:59 AM to 03:00:00 AM.
– Values from 02:00:00 AM to 02:59:59 AM are not valid.
**Last Sunday in October**
– Time jumps from 02:00:00 AM to 01:00:01 AM.
– Values from 01:00:01 AM to 02:00:00 AM are ambiguous because they are visited twice.
