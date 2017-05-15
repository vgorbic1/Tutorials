## Filters
Filter accepts textual data from a program or a file and then transforms it in a particular way. Filters do not change the original data.
To prin the first so many lines of input:
```
head -3 data.txt
```
The default is 10 lines.
To print the last so many lines of input:
```
tail -4 data.txt
```
The default is 10 lines.

### Sort
To sort the data (default is alphabetically):
```
sort filename
```
By defautl, sort uses a whitespace as a delimiter. To change a delimiter and select a column to display:
```
sort -t ',' -k 4 filename
```
To sort in a reverse order:
```
sort -r filename
```
To sort numerical data in a file:
```
sort -n filename
```
To sort numerical data in a human-readable format:
```
sort -h filename
```
### Other
To count number of lines of imput:
```
nl data.txt
```
To count lines (-l), words(-w), or characters(-m):
```
wc -l filename
```
To count everything and displya all together:
```
wc filename
```
To separate data in columns:
```
cut fileme
```
The command looks for a tab delimiter by default. 

To extract the first and third colmns:
```
cut -f 1,3 filename
```
To extract from the first to third column:
```
cut -f 1-3 filename
```
To extract from the first column in a comma delimited file:
```
cut -d ',' -f 1 filename
```
To remove duplicate lines that are one after another:
```
uniq filename
```
### Substitution
To substitute one character with others use "tr":
```
echo "H.P.Love" | tr a-z A-Z
```
This was the old way. Now use these classes instead:

Class | Chars
-- | --
[:alnum:] | A-Z a-z 0-9
[:alpha:] | A-Z a-z
[:blank:] | space and tab
[:digit:] | 0-9
[:lower:] | a-z
[:punct:] | punctuation and symbols
[:space:] | space, tab, newline, vertical whitespace
[:upper:] | A-Z

The new way will be:
```
echo "H.P.Love" | tr [:lower:][:upper:]
```
To replace repeated characters with a single instance (if you have two blanks, make it one):
```
tr -s[:blank:] < filename
```
You cannot write the file name directly when using "tr"!
```
WRONG!
tr -s [:blank:] fiename
```
To delete matching characters:
```
tr -d '-' < filename;
```
