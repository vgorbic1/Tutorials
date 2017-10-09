## Insertion Sort
*The insertion sort is a simple sorting algorithm, but it is usually
not the most efficient. To sort a list with n elements, the insertion sort begins with the second
element. The insertion sort compares this second element with the first element and inserts it
before the first element if it does not exceed the first element and after the first element if it
exceeds the first element. At this point, the first two elements are in the correct order. The third
element is then compared with the first element, and if it is larger than the first element, it is
compared with the second element; it is inserted into the correct position among the first three
elements.*
### Example
Put the elements of the list `3, 2, 4, 1, 5` in increasing order.
- The insertion sort first compares 2 and 3. Because 3 > 2, it places 2 in the first position,
producing the list `*2, 3,* 4, 1, 5`. At this point, 2 and 3 are in the correct order. 
- Next, it inserts the third element, 4, into the already sorted part of the list
by making the comparisons 4 > 2 and 4 > 3. Because 4 > 3, 4 remains in the third position.
At this point, the list is `*2, 3, 4,* 1, 5` and we know that the ordering of the first three elements
is correct. 
- Next, we find the correct place for the fourth element, 1, among the already sorted
elements, 2, 3, 4. Because 1 < 2, we obtain the list `*1, 2, 3, 4,* 5`. 
- Finally, we insert 5 into the correct position by successively comparing it to 1, 2, 3, and 4. 
Because 5 > 4, it stays at the end of the list, producing the correct order for the entire list.
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
