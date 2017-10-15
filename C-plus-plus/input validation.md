## Input Validation

### Using the while Loop for Input Validation
The while loop can be used to create input routines that repeat until
acceptable data is entered:
```c++
cout << "Enter a number in the range 1-100: ";
cin >> number;
while (number < 1 || number > 100)
{
  cout << "ERROR: Enter a value in the range 1-100: ";
  cin >> number;
}
```
### Using ASCII values
ASCII Values of Commonly Used Characters:
```
‘0’ – ‘9’   48 – 57
‘A’ – ‘Z’   65 – 90
‘a’ – ‘z’   97 – 122
blank       32
period      46
```
This program demonstrates how characters can be compared with the relational operators:
```c
#include <iostream>
using namespace std;

int main() {
 char ch;
 Get a character from the user.
 cout << "Enter a digit or a letter: ";
 ch = cin.get();
 
 // Determine what the user entered.
 if (ch >= '0' && ch <= '9')
  cout << "You entered a digit.\n";
 else if (ch >= 'A' && ch <= 'Z')
  cout << "You entered an uppercase letter.\n";
 else if (ch >= 'a' && ch <= 'z')
  cout << "You entered a lowercase letter.\n";
 else
  cout << "That is not a digit or a letter.\n";
 return 0;
}
```
