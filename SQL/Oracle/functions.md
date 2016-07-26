## SINGLE-ROW FUNCTIONS
A function is a predefined block of code that accepts one or more arguments inside parentheses and returns a single value as an output.
Single-row functions return one row of results.
Single-row functions can be nested one in another (used as an argument for another function).

### CASE CONVERSION FUNCTIONS
They alter the case of a character string and do not affect the data.

#### LOWER()
Convert character string to the lower case.
```
WHERE LOWER(lastname)  = ‘nelson’
``` 
(converts each field in lastname column to lower case, compares with the string within ‘ ‘ and displays the result found as the data originally stored in the column)
```
SELECT LOWER(lastname)
``` 
shows all data in lastname column in lower case.

#### UPPER()
Convert character string to the upper case.
```
WHERE UPPER(lastname)  = ‘UPPER’
```
(converts each field in lastname column to upper case, compares with the string within ‘ ‘ and displays the result found as the data originally stored in the column)
```
SELECT UPPER (lastname)
```
shows all data in lastname column in upper case.

#### INITCAP()
Converts character string to a mixed case, with each word beginning with a capital letter.
```
SELECT INITCAP(firstname)
```
displays the colun data with first characters as capital letters.

### CHARACTER MANIPULATION FUNCTIONS

#### SUBSTR()
Returns a portion of the original string.
```
SELECT DISTINCT SUBSTR(zip, 1, 3)
```
where zip is the column, 1 is the place where the needed string begins and 3 is the number of characters to show.
```
SELECT DISTINCT SUBSTR(zip, -3, 2)
```
negative means start count from the end of string.
```
WHERE SUBSTR(zip, -3, 2) < 30
```
filters the result based on the value of the zip code’s third and fourth digits.

Example: 
```
SUBSTR(‘HelloWorld’,1,5) results in: Hello
```

#### INSTR()
Searches a string for a specified set of characters or a substring, and returns a numeric value representing the first character position in which the substring is found. If not exists it returns 0.
It accepts two arguments: string value to search and the characters or substring (in single quotes) to locate.
By default search begins in the beginning of the string value and position of the first occurrence is located, but two optional arguments may specify these parameters.
```
SELECT INSTR(name, ‘,’) 
```
means: column, character to search. Return a the position of the first comma.
```
SELECT INSTR(name, ‘,’ , 1, 2)
```
means: column, character to search, start read position, occurrence.

Example: 
```
INSTR(‘HelloWorld’, ‘W’) results in: 6
```

#### LENGTH()
Tells the number of the characters in a string.
```
SELECT DISTINCT LENGTH(address)
```
“Distinct” eliminates duplicate values in the result.
```
ORDER BY LENGTH(address)
```
the smallest length on top.

Example:
```
LENGTH(‘HelloWorld’) results in: 10
```

#### LPAD() and RPAD()
Fill in the area to the left (or right) of the string with a specific character or even a blank space.
```
SELECT LPAD(firstname, 12, ‘ *’)
```
total length from left to right, the character in single quotes.

Example: 
```
LPAD(salary, 10, ‘*’) // results in: *****24000
RPAD(salary, 10, ‘*’) // results in: 24000*****
LPAD(‘ ‘,10,’*’) // results in: *********_        (where _ is a space) 
```

#### LTRIM() and RTRIM()
Removes a specific string of characters from the left (or right) side of data values.
```
SELECT LTRIM(address, ‘P.O. BOX’)
```
removes ‘P.O. BOX’ string from any value in address field.

#### TRIM()
Trims leading or trailing characters (or both) from a character string.

Example: 
```
TRIM(‘H’ FROM ‘HelloWorld’) results in: elloWorld
```

#### REPLACE()
Similar to search and replace function.
```
SELECT REPLACE(address, ‘P.O.’, ‘POST OFFICE’)
```
instead ‘P.O.’ in the address field will be ‘POST OFFICE’.

Example: 
```
REPLACE(‘JACK and JUE’, ‘J’, ‘BL’) results in: BLACK and BLUE
```

TRANSLATE()
Replaces a character in a string with a new one. Only one character!
SELECT TRANSLATE(name,  ‘,’, ‘-‘) instead each ‘,’ character in each name will be replaced with ‘-‘ character.
SELECT TRANSLATE(name, ‘PO’, ‘po’) each P will be changed to p, and each O will be changed to o.

CONCAT()
As (||), it concatenates data in two columns into one. Combines ONLY TWO columns and string literals. Use (||)! Or it is possible to nest one COCAT into another.
Example: CONCAT(‘Hello’, ‘World’) results in: HelloWorld

NUMBER FUNCTIONS

ROUND()
Rounds numeric fields to the stated precision.
Can also be used on date functions.
SELECT ROUND(retail, 2) two positions to the right of the point to round. 45,234 becomes 45,23
SELECT ROUND(retail, -2) two positions to the left of the point to round. 123,68 becomes 100

TRUNC()
Truncates numeric data.
SELECT TRUNC (retail, 2) two positions to the right of the point to truncate. 45.234 becomes 45.23
SELECT TRUNC (retail, -2) two positions to the left of the point to truncate. 193.68 becomes 100

MOD()
Returns only reminder of a division operation. Numerator and denominator needed. The modulus is shown.
Used to determine  whether a value is odd or even.
SELECT MOD(235,16) results in 11. (235/16 = 14 and 11/16)

ABS()
Returns absolute or positive value as a result, even if the result is negative.
SELECT ABS(pubdate-SYSDATE) even if the result should be negative the function shows positive value.

POWER()
Raises the first argument to the power as the second argument.
SELECT POWER(2, 3) results in 8. (2*2*2 gives 8)

DATE FUNCTIONS

The full date format of Oracle 11g: January 1, 4712 B.C. to December 31, 9999 A.D. Julian date numeric format.
To get the difference between dates the system converts the date into internal numeric format and then determines the difference.  To determine in terms of weeks divide the result by 7.
DATE datatype does not store time zone information. Only century, year, month, days, hours, minutes, and seconds. 
TIMESTAMP datatype stores time zone information as part of the data value.
RR (DD-MON-RR) format used to specify centuries:
Current Year	Given Date	RR	YY
1994	27-OCT-95	1995	1995
1994	27-OCT-17	2017	1917
2001	27-OCT-17	2017	2017
Date + number = Date (adds number of days to a date)
Date – number = Date (subtracts number of days from a date)
Date – Date = Number of Days! (subtracts one date from another)
Date + number / 24 = Date. Adds a number of hours to a date

MONTHS_BETWEEN() 
Shows number of months between two dates. Result can be positive or negative! If date1 is earlier than date2, the result is negative.
SELECT MONTHS_BETWEEN(orderdate, pubdte) result=pubdate-orderdate in months with decimal remainder.
Example: MONTHS_BETWEEN(’01-SEP-95’,’11-JAN-94’) results in: 19.6774194

ADD_MONTHS()
Displays the date after particular number of months added to the initial date. The argument should be an integer and can be negative, if you want to subtract month(s).
SELECT ADD_MONTHS(’01-DEC-08’,18) add 18 months to Dec 1, 2008.
Example: ADD_MONTHS (’31-JAN-96’,1) results in: ’29-FEB-96’

NEXT_DAY() 
Determines the next occurrence of a specific day of the week after given date. Can be a number or a char string.
SELECT NEXT_DAY(orderdate, ‘MONDAY’) if the date happens to be Monday too, the next Monday is returned.
Example: NEXT_DAY (’01-SEP-95’, ‘FRIDAY’) results in: ’08-SEP-95’

LAST_DAY()
Determines the last day of the month for a given date.
Example: LAST_DAY (’01-FEB-95’) results in: ’28-FEB-95’

ROUND()
Date rounds by unit of month or year to the nearest day, or by using a mask.
Months: if 16 or later – rounded up to the first of next month. If less than 16 – down to that month.
Years: if July 16 or later - rounded up to the first of next year. If less than July 16 – down to that year.
SELECT ROUND(pubdate, ‘MONTH’)  also can be spelled as ‘MM’
SELECT ROUND(pubdate, ‘YEAR’) also can be spelled as ‘YYYY’

TRUNC()
To return a number of (for example whole) months eliminating a decimal point when calculating the difference between two dates. Usually used with another function.
SELECT TRUNC(MONTHS_BETWEEN(orderdate, pubdate), 0) truncates to the whole month.

CURRENT_DATE
No parenthesis! Returns current date and time from the user session time zone.
SELECT CURRENT_DATE   - just a date
SELECT TO_CHAR(CURRENT_DATE, ‘DD-MON-YY HH:MM:SS’)    - date and time

SYSDATE 
No parenthesis! Returns current date and time from system where the database resides.
SELECT SYSDATE       - just a date
SELECT TO_CHAR(SYSDATE, ‘DD-MON-YY HH:MM:SS’)   - date and time

REGULAR EXPRESSIONS
Allow to describe complex patterns in textural data. Adhere to UNIX(POSIX) standards that defines an interface between programs and operating systems. Reg Exps increase the limits of LIKE operator that has only % and _. 
Reg Exp can search just a portion of the string, but LIKE operator works on the whole string at once.

REGEXP_LIKE()
Uses extended se of patterns for search. Attempts to search only part of entire value that match the pattern. If pattern is found the function shows entire record.
WHERE REGEXP_LIKE(description, ‘[0=9]{3}[-.][0-9]{3}[-.][0-9]{4}’)
[0-9]{3} Looking for a single character that must be a digit and repeats three times (three-digit number).
Then [-.] Looking for a hyphen or period, and so on.

REGEXP_SUBSTR()
Extends SUBSTR() function capabilities with pattern-matching operators. If pattern is found, the function shows only the matching substring. 
SELECT REGEXP_SUBSTR(description, ‘[0=9]{3}[-.][0-9]{3}[-.][0-9]{4}’)

OTHER FUNCTIONS

NVL()
Calculate with NULL values. Since a normal calculation with NULL produces only NULL as a result, this function substitutes the NULL with zero (0). Can be used with all data types, but all arguments must be of the same datatype as the resulting (final) argument!
SELECT salary+NVL(comission, 0)  -with NUMBER type
SELECT NVL(shipdate, ’06-APR-09’)-orderdate   -with DATE type
SELECT NVL(column_name_char, ‘Unavailable’)  -with CHAR type
SELECT NVL(TO_CHAR(column_name_numbers), ‘Unavailable’)  -with CHAR type, but numbers in column

NVL2()
If NULL value presents in the field, substitute it with the second parameter. In NULL value does not exist in the field, change it to the first parameter. Can be used with all data types. Logically equivalent to CASE expression.
SELECT NVL2(shipdate, ‘Shipped’, ‘Not Shipped’)

NULLIF()
Compares two values for equality. If two are equal, the function returns NULL value, if not equal the function returns the first of the two parameters. Often combined with NVL2 function to display descriptive status. Can be used with all data types.
SELECT NULLIF(paideach, retail)
SELECT NVL2( NULLIF(paidach, retail), ‘Sale Price’, ‘Regular Price’ )

COALESCE()
Returns the first non-null expression in the expression list. Can take multiple alternate values.  All expressions must be of one datatype.
SELECT COALESCE(TO_CHAR(commission_pct), TO_CHAR(manager_id), ‘No commission and no manager’)  -If commission_pct is NULL and manager_id is NULL, “No commission and no manager’ string will be returned. Apply TO_CHAR so all expressions are of one datatype (look at the last expression datatype).

IMPLICIT DATA CONVERSION
Automatic conversion by Oracle server (internal):
VARCHAR2 or CHAR to NUMBER (characters should represent a valid number)
VARCHAR2 or CHAR to DATE
NUMBER to VARCHAR2 or CHAR
DATE to VARCHAR2 or CHAR
Hire_date > ’01-JAN-90’ varchar2 or char implicitly converts to date

EXPLICIT DATA CONVERSION
Use conversion functions: TO_CHAR, TO_DATE, or TO_NUMBER:

TO_NUMBER()
Converts a value to a numeric datatype, if possible. If impossible – function returns an error.
SELECT TO_NUMBER(TO_CHAR(SYSDATE, ‘YYYY’))  -takes the year in date type, converts to char and then to number.

TO_CHAR()
Converts dates and numbers to a formatted character string. It is opposite of the TO_DATE function. 
When used on numeric data, any excess decimals are rounded (not truncated) to the specified in mask number of digits. Case-sensitive.
SELECT TO_CHAR(pubdate, ‘MONTH DD, YYYY’)
SELECT TO_CHAR(retail-cost, ‘$9999.99’)
SELECT TO_CHAR(salary, ‘fm$99,999.99’) results in: $24,000.   <= no decimal numbers, just a dot!
SELECT TO_CHAR(salary, ‘fm$99,999.00’) results in: $24.000.00

With Dates:
Element	Description
YEAR	Year, spelled out
YYYY	4-digit year
YYY
YY
Y	Last 3, 2, or 1 digit(s) of year.
IYY
IY
I	Last 3, 2, or 1 digit(s) of ISO year.
IYYY	4-digit year based on the ISO standard
Q	Quarter of year (1, 2, 3, 4; JAN-MAR = 1).
MM	Month (01-12; JAN = 01).
MON	Abbreviated name of month.
MONTH	Name of month, padded with blanks to length of 9 characters.
RM	Roman numeral month (I-XII; JAN = I).
WW	Week of year (1-53) where week 1 starts on the first day of the year and continues to the seventh day of the year.
W	Week of month (1-5) where week 1 starts on the first day of the month and ends on the seventh.
IW	Week of year (1-52 or 1-53) based on the ISO standard.
D	Day of week (1-7).
DAY	Name of day. (FRIDAY)
DD	Day of month (1-31).
DDD	Day of year (1-366).
DY	Abbreviated name of day.
J	Julian day; the number of days since January 1, 4712 BC.
HH	Hour of day (1-12).
HH12	Hour of day (1-12).
HH24	Hour of day (0-23).
MI	Minute (0-59).
SS	Second (0-59).
SSSSS	Seconds past midnight (0-86399).
FF	Fractional seconds.
. ,	Punctuation (DD, YYYY becomes 24, 2009)
“string”	Exact characters inside the double quotation marks (“ of “)
TH	Ordinal number (DDTH becomes 8th)
SP	Spells out the number (DDSP becomes EIGHT)
SPTH	Spells out the ordinal number (DDSPTH becomes EIGHTH)
AM or PM	Meridian indicator (also A.M. and P.M.)
FM	Fill Mode. Suppresses blank padding. (FMDay, becomes Friday,)
FX	Format Exact. Exact match for the character argument and date format model



With Numbers:
Element	Description	Example	Result
9	Numeric position	999999	123465
0	Display leading zeros	0999	0012
$	Floating dollar sign	$9999	$1234
L	Floating local currency	L9999	FF121
D	Returns decimal character in specified position	99D99	99.99
. 	Decimal point in position specified	9999.99	1234.78
G	Returns group separator	9G999	9,999
,	Comma in position specified	999,999	1,234
MI	Minus signs to right	99999	1234-
PR	Parenthesize negative elements	999999PR	<1234>
EEEE	Scientific notation	99.999EEE	1.234E+03
U	Returns currency in specified position	U9999	€1234
V	Multiply by 10 n times (n = number of 9s after V)	9999V99	123400
S	Returns negative or positive value	S9999	-1234 or +1234
B	Displays zero values as blank, not 0	B9999.99	1234.00

TO_DATE()
For users who are used to MM/DD/YY or Month DD, YYYY. It converts any format to Oracle 11g specific type:
MONTH (APRIL), MON (APR), MM (04), RM (IV), D(day of the week. Wednesday = 4), DD(day of the month 28), DDD (day of the year. December 31 = 365), DAY(day of the week. WEDNESDAY), DY (WED), YYYY (2009), YYY (2009 = 009), YY (2009 = 09), Y (2009 = 9), YEAR(TWO THOUSAND NINE), A.C. (2009 A.C.)
Frequently used with INSERT statements.
WHERE orderdate = TO_DATE(‘March 31, 2009’, ‘Month DD, YYYY’)
Use FX modifier to specify exact match of the character argument and date format model (except for case). No extra blanks! Same number of digits!

DECODE()
Takes a specified value and compares it to values in a list. If match is found the specified result is returned, if not – a default result is returned, if no default – a NULL is returned. Saves from entering multiple statements. Similar to CASE or IF-THEN-ELSE statement.
SELECT DECODE(state, ‘CA’, .08,       if the state in state column is California put .08 to the “Tax” column
			‘FL’ .07,       if the state in state column is Florida put .07 to the “Tax” column
			           0) “Tax” if none of these states, put 0 to the “Tax” column

CASE Expression (not a function)
Similar to DECODE function, but provides more flexibility, allowing comparisons besides equality. Requires same datatype for all expressions inside!
SELECT ROUND(MONTHS_BETWEEN(’01-JUL-09’, hiredate)/12,2),
	CASE
	   WHEN (MONTHS_BETWEEN(’01-JUL-09’, hiredate)/12,2) < 4 THEN ‘Level 1’
	   WHEN (MONTHS_BETWEEN(’01-JUL-09’, hiredate)/12,2) < 8 THEN ‘Level 2’
	   WHEN (MONTHS_BETWEEN(’01-JUL-09’, hiredate)/12,2) < 12 THEN ‘Level 3’
	   ELSE ‘Level 4’
	END “Retail Level”
FROM employees;

SOUNDEX()
Searches for the results phonetically similar to the specified in each record. Used when a certain last name was spelled incorrectly when entered to database (‘I’ instead of ‘y’)
WHERE SOUNDEX(lastname) = SOUNDEX(‘smyth’)      -will find all “Smith” and “Smyth”

GROUP FUNCTIONS

Also called multiple-row functions or aggregate functions return one result per group of rows processed.
All group functions ignore NULL values except COUNT(*). To include NULL values nest NVL() function within a group function. A group function may have an optional DISTINCT keyword to include only unique numeric values in calculation. ALL keyword (default) calculates all values in the column.
If include non-aggregate column and aggregate function in one SELECT statement always use GROUP BY.
Group functions can be nested only to a depth of two, and if nested GROUP BY is mandatory.

SUM()
Calculates the total amount stored in a numeric field for a group of records. Works only with numeric data.
SELECT SUM(paideach) “Total Profit”

AVG()
Calculates the average of numeric values in a specific column. Include NVL function, if work with NULL for correct calculation of average. Can be used only with numeric data. Convert any type to numeric data  with TO_NUMBER()
SELECT AVG(retail-cost) “Average Profit”
SELECT AVG(NVL(bonus,0))

COUNT()
Count the total records meeting a specific condition, including those containing NULL values!
Has three formats: COUNT(*) counts all duplicates and NULLs, and satisfies condition in WHERE;
COUNT(expr) counts all duplicates and all non-NULL values, and satisfies condition in expr; 
COUNT(DISTINCT expr) counts non-duplicate, non-NULL values, and satisfies condition in expr.
SELECT COUNT(DISTINCT category)    -counts each different value found in the Category column
SELECT DISTINCT COUNT(category)    -only duplicate rows (not duplicate Category values) should be suppressed.
SELECT COUNT(*) FROM orders WHERE shipdate IS NULL    -counts all NULL values in shipdate column. Do not confuse this with COUNT(shipdate) … WHERE shipdate IS NULL, since NULLs will not be counted!

MAX()
Returns the largest value stored in the specific column. Can be used with any kind of data except LOB and LONG. It shows the first value that occurs when column is sorted in descending order. Most recent date is the highest value. Letter “Z” is of higher value than “A” 
With dates returns the most recent date in the field.
SELECT MAX(retail-cost) “Highest Margin” 

MIN()
Returns the lowest value stored in the specific column. 
Works with any kind of data too. (numeric, non-numeric, dates, but not LOB and LONG)
With dates returns the earliest date in the field.
SELECT MIN(pubdate)

STATISTICAL GROUP FUNCTIONS
Used to perform calculations for data analysis.

STDDEV()
Calculates the standard deviation for a specific column. In other words, how close each value in group of numbers is to the mean, or average, of the group? Based on normal distribution. Works only with numeric data.
SELECT category, COUNT(*), AVG(retail-cost), STDEV(retail-cost) FROM books GROUP BY category;
-	If the result is: average – 18.26; stddev – 11.2267, it means that 68% of books in particular category have profit between $7.03 ($18.26 - $11.23) and $29.49 ($18.26 + $11.23). It gives a picture of the profit range.
-	If you have 0 as a result it means there is only one record to process. (Not enough statistical data)

VARIANCE()
Determines how widely data is spread in the group. It is based on minimum and maximum values for a specified column. If the data is clustered together – variance is small, if it contains extreme values – the variance is larger.
Works only with numeric data.
SELECT category, VARIANCE(retail-cost), MIN(retail-cost), MAX(retail-cost) FROM books GROUP BY category;
-	If you have 0 as a result it means there is only one record to process. (Not enough statistical data)

