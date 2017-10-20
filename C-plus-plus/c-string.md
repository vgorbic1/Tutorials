## C-String
There
are two primary ways that strings are stored in memory: as string objects, or as C-strings.

In C++, a C-string is a sequence of characters stored in consecutive memory
locations, terminated by a null character (or null terminator) `\0`. The purpose of 
the null terminator is to mark the end of the C-string:
```
"Do you want to see the message again? "
```

### C-String in Arrays
The C programming language does not provide a string class like the one that C++ provides.
In the C language, all strings are treated as C-strings.
When a C programmer wants to
store a string in memory, he or she has to create a char array that is large enough to hold
the string, plus one extra element for the null character.
```
const int SIZE = 21;
char name[SIZE] = "Jasmine";
```
After this code executes, the name array will be created with 21 elements. The first 8 elements
will be initialized with the characters 'J' , 'a' , 's' , 'm' , 'i' , 'n' , 'e' , and '\ 0'.
The null character is automatically added as the last character.

You can implicitly size a
char array by initializing it with a string literal, as shown here:
```
char name[] = "Jasmine";
```
After this code executes, the name array will be created with 8 elements, initialized with the
characters 'J' , 'a' , 's' , 'm' , 'i' , 'n' , 'e' , and '\ 0'.

### C-String with cin
C-string input can be performed by the cin object. The following code allows
the user to enter a string (with no whitespace characters) into the name array:
```
const int SIZE = 21;
char name[SIZE];
cin >> name;
```
The following statement uses cin’s `getline` member function to get a line of input (including
whitespace characters) and store it in the line array:
```
const int SIZE = 80;
char line[SIZE];
cin.getline(line, SIZE);
```
- The first argument tells getline where to store the string input. This statement indicates
the starting address of the line array as the storage location for the string. 
- The second argument indicates the maximum length of the string, including the null terminator.
```
// Display the input one character at a time.
cout << "The sentence you entered is:\n";
while (line[count] != '\0')
{
  cout << line[count];
  count++;
}
```
### Library Functions
These functions all require the `cstring` header file to be included:
```
#include <cstring>
```
- **strlen** determines the length of the string stored in the name array:
```
char name[] = "Thomas Edison";
int length;
length = strlen(name);
// output: 13
```
It doesn’t know where the array ends, so it looks for the null terminator to indicate the
end of the string.
- **strcat** concatenates or appends one string to another:
```
const int SIZE = 13;
char string1[SIZE] = "Hello ";
char string2[] = "World!";

strcat(string1, string2);
cout << string1 << endl;
// output: Hello World!
```
The function copies the contents of string2 to the end of string1.
If the array holding the first string isn’t large enough to hold both
strings, strcat will overflow the boundaries of the array!
Here is a program segment that uses the sizeof operator to test an array’s size before
strcat is called:
```
if (sizeof(string1) >= (strlen(string1) + strlen(string2) + 1))
  strcat(string1, string2);
else
  cout << "String1 is not large enough for both strings.\n";
```
- **strcpy** copyes one string to another:
```
const int SIZE = 13;
char name[SIZE];
strcpy(name, "Albert Einstein");
```
The array specified by the first argument will be overflowed if it isn’t large enough to hold
the string specified by the second argument.
