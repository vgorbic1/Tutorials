## Wildcards
Wildcards may be used at any part of a path
```
*   zero or more characters
?   single character
[ ] range of characters
^   not
```
To show everything in this directory:
```
ls directoryname*
```
To list all files with extesion .txt in the current directory:
```
ls *.txt
```
To list a file where the second character is "i" in the current dirrectory:
```
ls ?i*
```
To list files that have three characters in their extension:
```
ls *.???
```
To list files that have a dgit in their name:
```
ls *[0-9]*
```
To list files that does not begin whith any letter from "a" to "k" in their name:
```
ls [^a-k]*
```
