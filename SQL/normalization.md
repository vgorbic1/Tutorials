## Normalization
Normaliziation is removing anomalies:
- INSERTION Cannot enter data. Data is missing.
- UPDATE Same info must be updated in several places.
- DELETION deleting of information removes other data.

#### FIRST NORMAL FORM (1NF)
-	Remove all repeating groups (columns) 
-	Each attribute contains only one single value of single type. No commas!
-	Each row is unique

WAS:

ID	| FIRST NAME |	LAST NAME |	PHONE |	CHILD 1	| CHILD 2 |	CHILD 3
--- | --- | --- | --- | --- | --- | --- |
1 |	John |	Smith |	608 678-9999 |	Bill |	James |	Mark
2	| Mike	|Kern	|608 958-9090| | |			
3	| Sam	|Stevens	|608 956-2345	|Eugene | | 	

BECAME:

ID|	FIRST NAME|	LAST NAME|	PHONE
--- | --- | --- | --- 
1	|John	|Smith	|608 678-9999
2	|Mike	|Kern|	608 958-9090
3	|Sam|	Stevens|	608 956-2345

ID|	SEQENCE	|CHILD
--- | --- | --- 
1	|1	|Bill
1	|2	|James
1	|3	|Mark
3	|1	|Eugene

#### SECOND NORMAL FORM (2NF)
-	Remove Functional Dependencies (groups of repeated attributes that form subthemes)
-	All attributes should be dependent on the key, not on each other
-	No partial dependencies on concatenated keys.

WAS:

PERSON ID	|PERSON NAME	|PROJECT ID	|PROJECT NAME	|PROJECT PHONE
--- | --- | --- | --- | --- 
1	|John	|PR1	|Web Project	|666-666-6666
2	|Peter	|PR1	|Web Project	|666-666-6666
1	|John	|PR2	|Multimedia	|777-777-7777
3	|Sam	|PR2	|Multimedia	|777-777-7777

BECAME:

PERSON ID	| PERSON NAME
--- | ---
1	| John
2	| Peter
3	| Sam

PROJECT ID	| PROJECT NAME	| PROJECT PHONE
--- | --- | ---
PR1	|Web Project	|666-666-6666
PR2	|Web Project	|777-777-7777

PERSON ID	| PROJECT ID
--- | ---
1	|1
2	|1
3	|2

#### THIRD NORMAL FORM (3NF)
-	Remove Transient Dependencies (attributes  that depends on another attribute, but not on the key)

WAS

Person ID	| CITY |	COUNTRY
--- | --- | ---
1|	Los Angeles	|USA
2	|Los Angeles	|USA
3	|Los Angeles	|USA
4	|New York	|USA
5	|New York	|USA

COUNTRY depends on CITY only, but not on the primary key PERSON ID

BECAME:

Person ID	| CITY
--- | ---
1	|Los Angeles
2	|Los Angeles
3	|Los Angeles
4	|New York
5	|New York

CITY |	COUNTRY
--- | ---
Los Angeles	| USA
