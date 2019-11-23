## Data Types:

### Floating Point Datatypes
Single precision float 4 bytes. Numbers between ±3.4E-38 and ±3.4E38

Double precision double 8 bytes. Numbers between ±1.7E-308 and ±1.7E308

Long double precision long double 8 bytes*. Numbers between ±1.7E-308 and ±1.7E308

### auto
C++ 11 introduces an alternative way to define variables, using the auto key word and an
initialization value:
```c
auto amount = 100;
```
The `auto` key word tells the compiler to determine the variable’s data type from the initialization value.

### sizeof
The sizeof operator may be used to determine the size of a data type on any system:
```c
cout << "The size of an integer is " << sizeof(int);
```

### Casting
Type casting allows you to perform manual data type conversion.
```c
int books; // Number of books to read
int months; // Number of months spent reading
double perMonth; // Average number of books per month
perMonth = static_cast<double>(books) / months;
```
