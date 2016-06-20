##Regular Expressions
Regular expressions and wildcards are not the same.
#### egrep
Egrep prints every line which contains a given pattern. egrep is 100% equivalent to grep -E. As for what they do, -E switches grep into a special mode so that the expression is evaluated as an ERE (Extended Regular Expression) as opposed to its normal pattern matching.

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
