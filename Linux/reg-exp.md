##Regular Expressions
Regular expressions and wildcards are not the same.
#### egrep
Egrep prints every line whicn contains a given pattern.

To print all lines tha have word "melon" in it:
```
grep 'melon' filename
```
Regular expression symbols:
```
.     a single character
?     the preceding character matches 0 or 1 time
*     the preceding character matches 0 or more times
+     the preceding character matches 1 or more times
{n}   the preceding character matches exactly n times
{n,m} the preceding character matches at least n, but no more than m times
[abc] the characters included into the []
()    group of several characters to behave as one
|     cononical "OR"
^     matches the beginning of the line
$     matches the end of line
```
