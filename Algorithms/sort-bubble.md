## Bubble Sort
*The bubble sort is one of the simplest sorting algorithms, but not one
of the most efficient. It puts a list into increasing order by successively comparing adjacent
elements, interchanging them if they are in the wrong order.*

![bs]()

### Pseudocode
```
procedure bubblesort(a1, . . . , an : real numbers with n ≥ 2)
for i := 1 to n − 1
  for j := 1 to n − i
    if aj > aj+1 then interchange aj and aj+1
{a1, . . . , an is in increasing order}
```
