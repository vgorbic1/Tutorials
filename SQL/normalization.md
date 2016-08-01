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
 | ID	| FIRST NAME |	LAST NAME |	PHONE	CHILD 1	| CHILD 2 |	CHILD 3 |
 | --- | --- | --- | --- | --- | --- |
| 1 |	John |	Smith |	608 678-9999 |	Bill |	James |	Mark |
| 2	| Mike	|Kern	|608 958-9090| | | |			
| 3	| Sam	|Stevens	|608 956-2345	|Eugene | | |		

ID	SEQENCE	CHILD
1	1	Bill
1	2	James
1	3	Mark
3	1	Eugene
BECAME:
ID	FIRST NAME	LAST NAME	PHONE
1	John	Smith	608 678-9999
2	Mike	Kern	608 958-9090
3	Sam	Stevens	608 956-2345

