## PROGRAMMING LANGUAGE (PL / SQL)
A PL/SQL block is a set of procedural code (i.e. a program) that will execute and do whatever it is programmed to do. Unlike stand-alone SELECT statements, a SELECT statement in a PL/SQL block will not automatically send results back to the screen. Blocks can be given names and stored on the server in the Oracle database, much like views are objects in the database.  However, “anonymous” blocks are stored as files on user’s drive.

#### Declaring variables

Example:
```
DECLARE
  c_bonus_percent CONSTANT NUMBER(2,1) := 0.2; “:=” is PL/SQL assignment operator to specify the value.
  v_last_name     employees.last_name%TYPE; %TYPE tells Oracle that we wish the v_last_name variable to automatically have the same datatype as the last_name field in the Employees table.  
  v_salary        employees.salary%TYPE;
  v_bonus_amt     NUMBER(10,3);
```
To specify that all the column datatypes from one row should be returned one can use the keyword %ROWTYPE.  This returns a record composed of each column datatype.

Example:
```
DECLARE v_employees_rec employees%ROWTYPE;
```

#### Procedural Code

Example:
```
BEGIN
 SELECT last_name, salary, salary * c_bonus_percent
 INTO v_last_name, v_salary, v_bonus_amt
 FROM employees
 WHERE employee_id = 100;
 DBMS_OUTPUT.PUT_LINE ('The bonus for ' || v_last_name || ' is $' || v_bonus_amt); PUT_LINE can output both variable contents and literals.  
END;
```

#### System-Defined Exception Handling

Example:
```
DECLARE
  c_bonus_percent CONSTANT	 NUMBER(2,1):= 0.2;
  v_last_name employees.last_name%TYPE;
  v_salary employees.salary%TYPE;
  v_bonus_amt NUMBER(10,3);
BEGIN
  SELECT last_name, salary, salary * c_bonus_percent
  INTO v_last_name, v_salary, v_bonus_amt
  FROM employees
  WHERE employee_id = 500;
  DBMS_OUTPUT.PUT_LINE ( 'The bonus for ' || v_last_name || ' is $' ||    v_bonus_amt );
  EXCEPTION
	WHEN NO_DATA_FOUND THEN
	DBMS_OUTPUT.PUT_LINE ('The bonus cannot be calculated because there is no    employee with the requested ID in the employees table');
END;
```

#### Programmer-Defined Exception Handling
```
DECLARE
  c_bonus_percent CONSTANT	NUMBER(2,1):= 0.2;
  v_last_name employees.last_name%TYPE;
  v_salary employees.salary%TYPE;
  v_bonus_amt NUMBER(10,3);
  bonus_negative EXCEPTION; /* programmer-defined exception */
BEGIN
  SELECT last_name, salary, salary * c_bonus_percent
  INTO v_last_name, v_salary, v_bonus_amt
  FROM employees
  WHERE employee_id = 500;
    IF v_bonus_amt < 0	/* fatal error if bonus is negative */
    THEN RAISE bonus_negative; The RAISE statement stops normal execution of a PL/SQL block or subprogram and transfers control to an exception handler. 
    END IF;
  DBMS_OUTPUT.PUT_LINE ('The bonus for ' || v_last_name || ' is $' ||  v_bonus_amt);
  EXCEPTION
    WHEN NO_DATA_FOUND THEN
    BEGIN
      DBMS_OUTPUT.PUT_LINE ('Oracle code =' || SQLCODE);
      DBMS_OUTPUT.PUT_LINE ('Oracle message =' || SQLERRM);
      DBMS_OUTPUT.PUT_LINE ('The bonus cannot be calculated because there is no     employee with the requested ID in the employees table');
    END;
    WHEN bonus_negative THEN /* start of programmer-defined except */
    DBMS_OUTPUT.PUT_LINE ('The bonus cannot be negative - call supervisor immediately');	
    END;
```

#### Linearly Nested IF
```
DECLARE
   c_bonus_percent CONSTANT	 NUMBER(2,1) := 0.2;
   v_last_name employees.last_name%TYPE;
   v_salary employees.salary%TYPE;
   v_bonus_amt NUMBER(10,3);
   v_department_id employees.department_id%TYPE;
   bonus_negative EXCEPTION;          
BEGIN
  SELECT last_name, salary, department_id	       
  INTO v_last_name, v_salary, v_department_id
  FROM employees
  WHERE employee_id = 100;
   IF v_department_id = 90 THEN
      v_bonus_amt:= v_salary * c_bonus_percent; 
   ELSIF v_department_id = 60 THEN
	v_bonus_amt:= (v_salary - 500) * c_bonus_percent;
   ELSE
     v_bonus_amt:= (v_salary - 1000) * c_bonus_percent;
   END IF; END IF is two words
END;
```

#### Basic Loops 
```
DECLARE v_bonus_percent NUMBER(2,1) := 0.2;
   v_last_name employees.last_name%TYPE;
   v_salary employees.salary%TYPE;
   v_bonus_amt NUMBER(10,3);
BEGIN --anonymous block
SELECT last_name, salary      
  INTO v_last_name, v_salary
  FROM employees
  WHERE employee_id = 100;
LOOP                                                                                                                             
    v_bonus_amt  :=   v_salary * v_bonus_percent;                   
    DBMS_OUTPUT.PUT_LINE
       ( 'The bonus for ' || v_last_name || ' if a bonus percent of ' ||
           v_bonus_percent  || ' was applied to his/her salary of $' ||
      v_salary || ' would be $' || v_bonus_amt); /* reformatted output */        
    v_bonus_percent  :=  v_bonus_percent  +  0.1 ;   
    EXIT WHEN v_bonus_percent  > 0.5;         
END LOOP;                                                        
END;
```

#### While Loops
```
DECLARE v_bonus_percent NUMBER(2,1) :=  0.2;
  v_last_name employees.last_name%TYPE ;
  v_salary employees.salary%TYPE ;
  v_bonus_amt NUMBER(10,3);
BEGIN --anonymous block
  SELECT    last_name,  salary
       INTO  v_last_name, v_salary
       FROM  employees
       WHERE  employee_id = 100 ;
  WHILE (v_bonus_percent <= 0.5) LOOP /* start of loop */
        v_bonus_amt :=  v_salary  *  v_bonus_percent ;
        DBMS_OUTPUT.PUT_LINE
( 'The bonus for ' || v_last_name || ' if a bonus percent of ' ||
v_bonus_percent || ' was applied to his/her salary of $' ||
v_salary || ' would be $' || v_bonus_amt );
        v_bonus_percent  :=  v_bonus_percent + .1;
  END LOOP;                                /* end of loop */
END;
```

#### An Explicit Cursor With Multiple Rows
```
DECLARE v_bonus_percent CONSTANT NUMBER(2,1) := 0.2;
   v_last_name employees.last_name%TYPE;
   v_salary employees.salary%TYPE;
   v_bonus_amt NUMBER(10,3);
   v_department_id employees.department_id%TYPE;
   CURSOR emp_cursor IS
      SELECT last_name, salary, department_id     
      FROM    employees
      WHERE   department_id = 50;
BEGIN
  OPEN emp_cursor; /* this executes the SELECT statement */
  LOOP                                                                   
  FETCH emp_cursor INTO   v_last_name,  v_salary,  v_department_id;
  EXIT WHEN emp_cursor%NOTFOUND;                                             
     v_bonus_amt :=   v_salary * v_bonus_percent;                   
     DBMS_OUTPUT.PUT_LINE
       ('The bonus for ' || v_last_name || ' of dept ' || v_department_id ||
         ' if a bonus percent of ' ||
           v_bonus_percent || ' was applied to his/her salary of $' ||
      v_salary || ' would be $' || v_bonus_amt);       /* reformatted output */         
  END LOOP; 
  IF emp_cursor%ROWCOUNT > 0 THEN
      DBMS_OUTPUT.PUT_LINE
    ('—Block ran to completion—normal termination');
  ELSE
      DBMS_OUTPUT.PUT_LINE
    ('—No rows in cursor—block terminated without processing rows');
  END IF;
  CLOSE emp_cursor;
END;
```
