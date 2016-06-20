##Regular Expressions
Regular expressions and wildcards are not the same.
####grep
Grep (Global Regular Expressions Print) is a program which scans a specified file or files line by line, returning lines that contain a pattern. A pattern is an expression that specifies a set of strings by interpreting characters as meta-characters. This enables users to type a short series of characters and meta characters into a grep command to have the computer show us what lines in which files match. Some common flags are: -c for counting the number of successful matches and not printing the actual matches, -i to make the search case insensitive, -n to print the line number before each match printout, -v to take the complement of the regular expression (i.e. return the lines which don't match), and -l to print the file names of files with lines which match the expression.

#### egrep
Egrep prints every line which contains a given pattern. egrep is 100% equivalent to grep -E. As for what they do, -E switches grep into a special mode so that the expression is evaluated as an ERE (Extended Regular Expression) as opposed to its normal pattern matching.

To print all lines tha have word "melon" in it:
```
egrep 'melon' filename
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
