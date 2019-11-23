## Pointers
On a PC, for instance, it’s common for one byte 
(8 bits) to be allocated for chars, two bytes for shorts, four bytes for ints, longs, and floats, and eight bytes
for doubles. Each byte of memory has a unique address. The address operator `&` returns the memory address of a variable.
A variable’s address is the address of the first
byte allocated to that variable. To displays the variable’s address on the screen:
```c++
cout << &amount;
```
The address of the variable x is displayed in hexadecimal.

**Pointer variables**, which are often just called **pointers**, are designed
to hold memory addresses. With pointer variables you can indirectly
manipulate data stored in other variables.

Pointer variables are similar to reference variables, but pointer variables
operate at a lower level.

In C++, pointers are useful, and even necessary, for many
operations. One such operation is dynamic memory allocation.
When you are writing a
program that will need to work with an unknown amount of data, dynamic memory allocation
allows you to create variables, arrays, and more complex data structures in memory
while the program is running. Pointers are also very useful in algorithms that manipulate arrays and work
with certain types of strings. In object-oriented programming pointers are very useful for creating and working with objects
and for sharing access to those objects. The real benefit of pointers is that they allow you to indirectly access and modify 
the variable being pointed to.

The definition of a pointer variable:
```c++
int *ptr;

// reads as "ptr is a pointer to an int".
```
The asterisk (*indirection operator*) in front of the variable name indicates that `ptr` is a pointer variable. The `int`
data type indicates that `ptr` can be used to hold the address of an integer variable. 
In this definition, the word `int` does not mean that `ptr` is an integer variable.
It means that `ptr` **can hold** the address of an integer variable. Pointers only
hold one kind of value: an address.

It is never a good idea to define a pointer variable without initializing it with a valid memory
address. For that reason, it is a good idea to initialize pointer
variables with the special value `nullptr`. In C++ 11, the nullptr key word was introduced to represent the address 0.
```c++
int *ptr = nullptr;
```
This statement assigns the address of the x variable to the ptr variable:
```c++
ptr = &x;
```
The full programm:
```c++
int x = 25; // int variable
int *ptr = nullptr; // Pointer variable, can point to an int

ptr = &x; // Store the address of x in ptr

// Use both x and ptr to display the value in x.
cout << "Here is the value in x, printed twice:\n";
cout << x << endl; // Displays the contents of x
cout << *ptr << endl; // Displays the contents of x

// Assign 100 to the location pointed to by ptr. This
// will actually assign 100 to x.
*ptr = 100;

// Use both x and ptr to display the value in x.
cout << "Once again, here is the value in x:\n";
cout << x << endl; // Displays the contents of x
cout << *ptr << endl; // Displays the contents of x
```
Pointers may be defined in the same statement as other variables of the same type:
```
int myValue, *pint = &myValue;
```
### Pointers and Arrays
Array names can be used as constant pointers, and pointers can be used
as array names.
```c++
// This program shows an array name being dereferenced with the * operator.
#include <iostream>
using namespace std;

int main()
{
  short numbers[] = {10, 20, 30, 40, 50};

  cout << "The first element of the array is ";
  cout << *numbers << endl;
  return 0;
}
```
If the expression
`*numbers`, which is the same as `*(numbers + 0)`, retrieves the first element in the array,
then `*(numbers + 1)` retrieves the second element.

The parentheses are critical when adding values to pointers. The `*` operator
has precedence over the `+` operator, so the expression `*number + 1` is not equivalent to
`*(number + 1)`. `*number + 1` adds one to the contents of the first element of the array,
while `*(number + 1)` adds one to the address in number, then dereferences it.
```c++
// This program processes an array using pointer notation.
#include <iostream>
using namespace std;

int main()
{
  const int SIZE = 5; // Size of the array
  int numbers[SIZE]; // Array of integers
  int count; // Counter variable
  
   // Get values to store in the array.
   // Use pointer notation instead of subscripts.
   cout << "Enter " << SIZE << " numbers: ";
   for (count = 0; count < SIZE; count++)
     cin >> *(numbers + count);
  
   // Display the values in the array.
   // Use pointer notation instead of subscripts.
   cout << "Here are the numbers you entered:\n";
   for (count = 0; count < SIZE; count++)
     cout << *(numbers + count)<< " ";
   cout << endl;
   return 0;
 }
 ```
```
array[index] is equivalent to *( array + index )
```
C++ performs no bounds checking with arrays! When
stepping through an array with a pointer, it’s possible to give the pointer an address
outside of the array. 

Array names are pointer constants . You can't make them point to anything but the array
they represent:
```
double readings[20], totals[20];
double *dptr = nullptr;

// These statements are legal:
dptr = readings; // Make dptr point to readings.
dptr = totals; // Make dptr point to totals.

// But these are illegal:
readings = totals; // ILLEGAL! Cannot change readings.
totals = dptr; // ILLEGAL! Cannot change totals.
```
Pointers may be defined in the same statement as an array of the same type:
```
double readings[50], *marker = readings;
```

### Pointer Arithmetic
Not all arithmetic operations may be performed on pointers. For example, you cannot
multiply or divide a pointer. The following operations are allowable:
- The ++ and −− operators may be used to increment or decrement a pointer variable.
- An integer may be added to or subtracted from a pointer variable. This may be performed
with the + and − operators, or the += and −= operators.
- A pointer may be subtracted from another pointer.
### Comparing Pointers
If one address comes before another address in memory, the first address
is considered `less than` the second. C++’s relational operators may be
used to compare pointer values. The capability of comparing addresses gives you another way 
to be sure a pointer does not go beyond the boundaries of an array.

Comparing two pointers is not the same as comparing the values the two
pointers point to:
```c++
// The following if statement compares the addresses
// stored in the pointer variables ptr1 and ptr2:
if (ptr1 < ptr2)

// The following statement, however, compares the values 
// that ptr1 and ptr2 point to:
if (*ptr1 < *ptr2)
```
This program uses a pointer to display the contents of an integer array:
```c++
#include <iostream>
using namespace std;

int main()
{
  int set[8] = {5, 10, 15, 20, 25, 30, 35, 40};
  int *nums = set; // Make nums point to set
  
  // Display the numbers in the array.
  cout << "The numbers in set are:\n";
  cout << *nums << " "; // Display first element
  while (nums < &set[7])
  {
    // Advance nums to point to the next element.
    nums++;
    // Display the value pointed to by nums.
    cout << *nums << " ";
  }

  // Display the numbers in reverse order.
  cout << "\nThe numbers in set backward are:\n";
  cout << *nums << " "; // Display first element
  while (nums > set)
  {
    // Move backward to the previous element.
    nums−−;
    // Display the value pointed to by nums.
    cout << *nums << " ";
  }
  return 0;
}
```
### Pointers as Function Parameters
A pointer can be used as a function parameter. It gives the function
access to the original argument, much like a reference parameter does.
Here is the definition of a function that uses a pointer parameter:
```c++
void doubleValue(int *val)
{
  *val *= 2;
}
```
Here is an example of a call to the `doubleValue` function:
```c++
doubleValue(&number);
```
Function prototype:
```c++
void getNumber(int *);
```
This statement uses the address operator `&`to pass the address of number into the `val`
parameter. After the function executes, the contents of number will have been multiplied by
two.
