## Formatting Output
The `cout` object provides ways to format data as it is being displayed. his affects the way data appears on the screen.
Include `<iomanip>` in order to use the formatting.

### setw()
A stream manipulator, `setw`, can be used to establish print fields of a specified width.
```c
#include <iomanip>
...
value = 23;
cout << "(" << setw(5) << value << ")";
...
output:
(   23)
```

### setprecision()
Floating-point values may be rounded to a number of significant digits , or precision , which
is the total number of digits that appear before and after the decimal point. You can control
the number of significant digits with which floating-point values are displayed by using
the `setprecision` manipulator.
```c
#include <iomanip>
...
quotient = 4.91877;
cout << quotient << endl;
cout << setprecision(5) << quotient << endl;
cout << setprecision(2) << quotient << endl;
cout << setprecision(1) << quotient << endl;
...
output:
4.91877
4.9188
5
```

### fixed
When the precision of a number is set to a lower value, numbers tend to be printed in scientific notation (1.4568e+005).
Another stream manipulator, `fixed`, forces cout to print the digits in fixed-point notation, or decimal.
```
cout << setprecision(2) << fixed;
```

### showpoint
If we want the numbers padded with trailing zeroes, we must use the `showpoint` manipulator.
```c
double x = 123.4, y = 456.0;
cout << setprecision(6) << showpoint << x << endl;
cout << y << endl;
```
These cout statements will produce the following output:
```
123.400
456.000
```

### left and right
The `left` manipulator remains in effect until you use the right (default) manipulator, which causes all subsequent output
to be right-justified.
```c
double x = 146.789, y = 24.2, z = 1.783;
cout << left << setw(10) << x << endl;
cout << setw(10) << y << endl;
cout << setw(10) << z << endl;
```
The output of these cout statements is:
```
146.789
 24.2
  1.783
```
