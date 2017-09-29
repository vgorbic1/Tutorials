## Arrays
The Standard Template Library offers a `vector` data type, which in
many ways, is superior to standard arrays.

An array works like a variable that can store a group of values, all of the same type. The
values are stored together in consecutive memory locations.
### Array Initialization
```
const int NUM_DAYS = 6;
int days[NUM_DAYS];

or

int days[6];
```
also
```
const int MONTHS = 12;
int days[MONTHS] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

or

string planets[SIZE] = { "Mercury", "Venus", "Earth", "Mars",
  "Jupiter", "Saturn", "Uranus", "Neptune", "Pluto (a dwarf planet)" };
```
It’s possible to only initialize part of an array, such as:
```
int numbers[7] = {1, 2, 4, 8};
```
If an array is partially initialized, the uninitialized elements will be set to zero.

It’s possible to define an array without specifying its size, as long as you provide an initialization
list. C++ automatically makes the array large enough to hold all the initialization
values:
```
double ratings[] = {1.0, 1.5, 2.0, 2.5, 3.0};
```
### Accessing Array Elements
```
hours[0] = 20;
```
### Loops
```
const int ARRAY_SIZE = 5;
int numbers[ARRAY_SIZE];
for (int count = 0; count < ARRAY_SIZE; count++)
  numbers[count] = 99;
```  
You can use the following range-based for loop to display the contents of the numbers array.
The range-based for loop can be used in any situation where you need to step through the
elements of an array, and you do not need to use the element subscripts. It will not work,
however, in situations where you need the element subscript for some purpose.
```
int numbers[] = { 3, 6, 9 };
for (int val : numbers)
  cout << val << endl;
```
### Arrays as Function Arguments
For an element of an array:
```
// Function prototype
void showValue(int);

// Function call
showValue(numbers[index]);

// Function definition
void showValue(int num)
{
  cout << num << " ";
}
```
For entire array:
For an element of an array:
```
// Function prototype
void showValues(int [], int);

// Array instatntiation
const int ARRAY_SIZE = 8;
int numbers[ARRAY_SIZE] = {5, 10, 15, 20, 25, 30, 35, 40};

// Function call
showValues(numbers, ARRAY_SIZE);

// Function definition
void showValues(int nums[], int size) {
  for (int index = 0; index < size; index++)
    cout << nums[index] << " ";
  cout << endl;
}
```
You can prevent a function from making
changes to an array argument by using the const key word in the parameter declaration:
```
void showValues(const int nums[], int size) {
  for (int index = 0; index < size; index++)
    cout << nums[index] << " ";
  cout << endl;
}
```
### Two-Dimensional Arrays
A two-dimensional array is like several identical arrays put together. It is
useful for storing multiple sets of data.
```
const int NUM_DIVS = 3; // Number of divisions
const int NUM_QTRS = 4; // Number of quarters
double sales[NUM_DIVS][NUM_QTRS]; // Array with 3 rows and 4 columns.
```
Inititalizing:
```
int hours[3][2] = {{8, 5}, {7, 9}, {6, 3}};
```
### Passing Two-Dimensional Arrays to Functions
```
// Function prototype
void showArray(const int [][COLS], int);

// Function call
showArray(table1, TBL1_ROWS);

// Function definition
void showArray(const int numbers[][COLS], int rows) {
  for (int x = 0; x < rows; x++) {
    for (int y = 0; y < COLS; y++) {
      cout << setw(4) << numbers[x][y] << " ";
    }
    cout << endl;
  }
}
```
