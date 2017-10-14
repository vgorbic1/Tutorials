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
