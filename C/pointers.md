## Pointers
Pointer is a variable that stores an address of another variable.
To declare a pointer to point to a variable with Integer (int) type:
```
int *p;
```
In C language a pointer takes 4 bytes of memory. 

To assign a variable to a pointer:
```
int a;
int *p; 
p = &a;
```
Now the pointer `p` holds the memory address of vairable `a`.
```
* - give me the value of ...
& - give me the memory address of ...
```
### In Arrays:
To get a memory address of an element of an array:
```
int A[3];
A + i = &A[i]
```
To get a value:
```
int A[3]; // where i = 3
A[i] = *(A+i)
```
