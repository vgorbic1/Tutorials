## Filters
Filter accepts testual data from a program or a file and then transforms it in a particular way. Filters do not change the original data.
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
To sort the data (default is alphabetically):
```
sort filename
```
To count number of lines of imput:
```
nl data.txt
```
To count lines (-l), words(-w), or characters(-m):
```
wc -l filename
```
To separate data in columns:
```
cut fileme
```
To remove duplicate lines that are one after another:
```
uniq filename
```
