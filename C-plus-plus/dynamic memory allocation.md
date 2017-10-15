## Dynamic Memory Allocation
Variables may be created and destroyed while a program is running.

What about those times when you don’t know how many variables you need? For
instance, suppose you want to write a test-averaging program that will average any number
of tests. Obviously the program would be very versatile, but how do you store the individual
test scores in memory if you don’t know how many variables to define?

Quite simply,
you allow the program to create its own variables “on the fly.” This is called dynamic
memory allocation and is only possible through the use of pointers.

To dynamically allocate memory means that a program, while running, asks the computer
to set aside a chunk of unused memory large enough to hold a variable of a specific data
type. Let’s say a program needs to create an integer variable. It will make a request to the
computer that it allocate enough bytes to store an int . When the computer fills this request,
it finds and sets aside a chunk of unused memory large enough for the variable. It then gives
the program the starting address of the chunk of memory. The program can only access the
newly allocated memory through its address, so a pointer is required to use those bytes.

The way a C++ program requests dynamically allocated memory is through the `new` operator.
Assume a program has a pointer to an int defined as
```
int *iptr = nullptr;
```
Here is an example of how this pointer may be used with the new operator:
```
iptr = new int;
```
This statement is requesting that the computer allocate enough memory for a new `int` variable.
The operand of the new operator is the data type of the variable being created. Once
the statement executes, `iptr` will contain the address of the newly allocated memory.
A value may be stored in this new variable by dereferencing the pointer:
```
*iptr = 25;
```
Any other operation may be performed on the new variable by simply using the dereferenced
pointer:
```
cout << *iptr; // Display the contents of the new variable.
cin >> *iptr; // Let the user input a value.
total += *iptr; // Use the new variable in a computation.
```
Although the statements above illustrate the use of the new operator, there’s little purpose
in dynamically allocating a single variable. A more practical use of the new operator is to
dynamically create an array. Here is an example of how a 100-element array of integers
may be allocated:
```
iptr = new int[100];
```
Once the array is created, the pointer may be used with subscript notation to access it. For
instance, the following loop could be used to store the value 1 in each element:
```
for (int count = 0; count < 100; count++)
iptr[count] = 1;
```
But what if there isn’t enough free memory to accommodate the request? What if the
program asks for a chunk large enough to hold a 100,000-element array of floats,
and that much memory isn’t available? When memory cannot be dynamically allocated,
C++ throws an exception and terminates the program.

When a program is finished using a dynamically allocated chunk of memory, it should
release it for future use. The `delete` operator is used to free memory that was allocated
with `new`. Here is an example of how delete is used to free a single variable, pointed to
by `iptr`:
```
delete iptr;
```
If `iptr` points to a dynamically allocated array, the `[]` symbol must be placed between
`delete` and `iptr`:
```
delete [] iptr;
```
Failure to release dynamically allocated memory can cause a program to have a memory
leak:
```
void grabMemory()
{
  const int SIZE = 100;
  // Allocate space for a 100-element array of integers.
  int *iptr = new int[SIZE];
  // The function ends without deleting the memory!
}
```
Notice that the function dynamically allocates a 100-element int array and assigns its
address to the iptr pointer variable. But then, the function ends without deleting the memory.
Once the function has ended, the `iptr` pointer variable no longer exists. As a result,
the program does not have a pointer to the dynamically allocated memory, therefore, the
memory cannot be accessed or deleted. It will sit unused as long as the program is running.

Only use pointers with delete that were previously used with new. If
you use a pointer with delete that does not reference dynamically allocated memory,
unexpected problems could result!

### Example
```c++
// This program totals and averages the sales figures for any
// number of days. The figures are stored in a dynamically
// allocated array.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
  double *sales = nullptr, // To dynamically allocate an array
  total = 0.0, // Accumulator
  average; // To hold average sales
  int numDays, // To hold the number of days of sales
  count; // Counter variable

  // Get the number of days of sales.
  cout << "How many days of sales figures do you wish ";
  cout << "to process? ";
  cin >> numDays;
  // Dynamically allocate an array large enough to hold
  // that many days of sales amounts.
  sales = new double[numDays];

  // Get the sales figures for each day.
  cout << "Enter the sales figures below.\n";
  for (count = 0; count < numDays; count++)
  {
    cout << "Day " << (count + 1) << ": ";
    cin >> sales[count];
  }
  
  // Calculate the total sales
  for (count = 0; count < numDays; count++)
  {
    total += sales[count];
  }

  // Calculate the average sales per day
  average = total / numDays;

  // Display the results
  cout << fixed << showpoint << setprecision(2);
  cout << "\n\nTotal Sales: $" << total << endl;
  cout << "Average Sales: $" << average << endl;

  // Free dynamically allocated memory
  delete [] sales;
  sales = nullptr; // Make sales a null pointer.

  return 0;
}
```
Program Output
```
How many days of sales figures do you wish to process? 5 [Enter]
Enter the sales figures below.
Day 1: 898.63 [Enter]
Day 2: 652.32 [Enter]
Day 3: 741.85 [Enter]
Day 4: 852.96 [Enter]
Day 5: 921.37 [Enter]
Total Sales: $4067.13
Average Sales: $813.43
```
