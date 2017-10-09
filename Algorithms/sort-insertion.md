## Insertion Sort
*The insertion sort is a simple sorting algorithm, but it is usually
not the most efficient. To sort a list with n elements, the insertion sort begins with the second
element. The insertion sort compares this second element with the first element and inserts it
before the first element if it does not exceed the first element and after the first element if it
exceeds the first element. At this point, the first two elements are in the correct order. The third
element is then compared with the first element, and if it is larger than the first element, it is
compared with the second element; it is inserted into the correct position among the first three
elements.*
### Pseudocode
```
procedure insertion sort(a1, a2, . . . , an: real numbers with n ≥ 2)
for j := 2 to n
  i := 1
  while aj > ai
    i := i + 1
  m := aj
  for k := 0 to j − i − 1
    aj−k := aj−k−1
  ai := m
{a1, . . . , an is in increasing order}
```
