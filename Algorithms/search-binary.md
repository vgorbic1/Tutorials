## Binary Search
*This algorithm can be used when the list has terms occurring in order of increasing size. It proceeds by comparing the element to be located to the middle term of
the list. The list is then split into two smaller sublists of the same size, or where one of these
smaller lists has one fewer term than the other. The search continues by restricting the search
to the appropriate sublist based on the comparison of the element to be located and the middle
term.*
### Example
To search for 19 in the list
```
1 2 3 5 6 7 8 10 12 13 15 16 18 19 20 22
```
first split this list, which has 16 terms, into two smaller lists with eight terms each, namely,
```
1 2 3 5 6 7 8 10     12 13 15 16 18 19 20 22
```
Then, compare 19 and the largest term in the first list. Because 10 < 19, the search for 19 can
be restricted to the list containing the 9th through the 16th terms of the original list. Next, split
this list, which has eight terms, into the two smaller lists of four terms each, namely,
```
12 13 15 16     18 19 20 22
```
Because 16 < 19 (comparing 19 with the largest term of the first list) the search is restricted to
the second of these lists, which contains the 13th through the 16th terms of the original list. The
list 18 19 20 22 is split into two lists, namely,
```
18 19     20 22
```
Because 19 is not greater than the largest term of the first of these two lists, which is also 19, the
search is restricted to the first list: 18 19, which contains the 13th and 14th terms of the original
list. Next, this list of two terms is split into two lists of one term each: 18 and 19. Because
18 < 19, the search is restricted to the second list: the list containing the 14th term of the list,
which is 19. Now that the search has been narrowed down to one term, a comparison is made,
and 19 is located as the 14th term in the original list.
### Pseudocode
```
procedure binary search (x: integer, a1, a2, . . . , an: increasing integers)
i := 1{i is left endpoint of search interval}
j := n {j is right endpoint of search interval}
while i < j
m := (i + j)/2
if x > am then i := m + 1
else j := m
if x = ai then location := i
else location := 0
return location{location is the subscript i of the term ai equal to x, or 0 if x is not found}
```
