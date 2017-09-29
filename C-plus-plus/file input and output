## File Input and Output
Just as cin and cout require the iostream file to be included in the program, C++ file
access requires another header file. The file `fstream` contains all the declarations necessary
for file operations. It is included with the following statement:
```c
#include <fstream>
```
The fstream header file defines the data types `ofstream`, `ifstream`, and `fstream`. Before
a C++ program can work with a file, it must define an object of one of these data types.

- *ofstream* Output file stream. You create an object of this data type when you
want to create a file and write data to it.
- *ifstream* Input file stream. You create an object of this data type when you
want to open an existing file and read data from it.
- *fstream* File stream. Objects of this data type can be used to open files for
reading, writing, or both.

### Creating a File Object and Opening a File
The following code shows an example of opening a file for input (reading).
```
ifstream inputFile;
inputFile.open("Customers.txt");
```
The following code shows an example of opening a file for output (writing).
```
ofstream outputFile;
outputFile.open("Employees.txt");
```
Often, when opening a file, you will need to specify its path as well as its name. For example,
on a Windows system the following statement opens the file `C:\data\inventory.txt`:
```
inputFile.open("C:\\data\\inventory.txt")
```
Notice the use of two backslashes in the file’s path. Two backslashes are
needed to represent one backslash in a string literal.

### Closing a File
```
inputFile.close();
```

### Writing Data to a File
```
outputFile << "I love C++ programming\n";
```

### Reading Data from a File
```
inputFile >> name;
```

### Using Loops to Process Files
```
// Open a file named Sales.txt.
outputFile.open("Sales.txt");
// Get the sales for each day and write it to the file.
for (int count = 1; count <= numberOfDays; count++) {
  // Get the sales for a day.
  cout << "Enter the sales for day " << count << ": ";
  cin >> sales;
  // Write the sales to the file.
  outputFile << sales << endl;
}
// Close the file.
outputFile.close();
```

### Detecting the End of the File
```
// Open the file.
 inputFile.open("ListOfNumbers.txt");
// Read the numbers from the file and display them.
while (inputFile >> number) {
  cout << number << endl;
}
// Close the file.
inputFile.close();
```

### Testing for File Open Errors
```
// Open the file.
inputFile.open("BadListOfNumbers.txt");
// If the file successfully opened, process it.
if (inputFile){
  // Read the numbers from the file and display them.
  while (inputFile >> number) {
    cout << number << endl;
  }
  // Close the file.
  inputFile.close();
} else {
  // Display an error message.
  cout << "Error opening the file.\n";
}
```
