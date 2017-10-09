## Linear Search (Sequential Search)
*Continue comparing term that is under the search successively with each term of the list until a match is found, where
the solution is the location of that term, unless no match occurs. If the entire list has been searched without locating x, the 
solution is 0.*
### Pseudocode
```
procedure linear search(x: integer, a1, a2, . . . , an: distinct integers)
i := 1
while (i ≤ n and x != ai )
  i := i + 1
  if i ≤ n then location := i
  else location := 0
return location {location is the subscript of the term that equals x, or is 0 if x is not found}
```
Write a function to find if the element is in the set, and if it is, return the location of it,
if not, return *-1*.
```c++
// C++
int linearSearch(int n)
{
    // define a set as an array
    int set[] = {1, 49, -8, 13, 38, 0, 2, 23};
    
    // find the size of the array
    int size = sizeof(set) / sizeof(set[0]);
    
    // search the set for the element
    int i = 0;
    while (i < size && set[i] != n) i++;
    
    // if all set was looped through and the element
    // was not found set it to -1
    if (i == size) i = -1;
        return i;
}
```
