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
Open file for reading and writing:
```
fstream dataFile;
dataFile.open ("Customers.txt", fstream::in | fstream::out);
```
To append to the data, that is already in the file:
```
fstream dataFile;
dataFile.open ("Customers.txt", fstream::in | fstream::app);
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
```c++
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
```c++
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
```c++
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
### Reading Data from a File into an Array
```c++
const int ARRAY_SIZE = 10; // Array size
int numbers[ARRAY_SIZE]; // Array with 10 elements
int count = 0; // Loop counter variable
ifstream inputFile; // Input file stream object

// Open the file.
inputFile.open("TenNumbers.txt");
// Read the numbers from the file into the array.
while (count < ARRAY_SIZE && inputFile >> numbers[count])
  count++;
// Close the file.
inputFile.close();
// Display the numbers read:
cout << "The numbers are: ";
for (count = 0; count < ARRAY_SIZE; count++)
  cout << numbers[count] << " ";
cout << endl;
```
Another way, if you know the maximum possible number of the elements in the array:
```c++
// Prototype
int countRecords(ifstream &, int[], int);

int main()
{
 // Create array of maximum size of records:
    const int SIZE = 100;
    int scores[SIZE];

    ifstream infile("data.txt");
    // Populate the array with records
    createArray(infile, scores, SIZE);
    infile.close();
    ...
}
void createArray(ifstream & file, int scores[], int size)
{
    int score;
    int num = 0;

    while (file >> score && num < size)
    {
        scores[num] = score;
        num++;
    }
}
```
### Writing the Contents of an Array to a File
```c++
const int ARRAY_SIZE = 10; // Array size
int numbers[ARRAY_SIZE]; // Array with 10 elements
int count; // Loop counter variable
ofstream outputFile; // Output file stream object
// Store values in the array.
for (count = 0; count < ARRAY_SIZE; count++)
  numbers[count] = count;
// Open a file for output.
outputFile.open("SavedNumbers.txt");
// Write the array contents to the file.
for (count = 0; count < ARRAY_SIZE; count++)
  outputFile << numbers[count] << endl;
// Close the file.
  outputFile.close();
```

C++ does not prevent you from overwriting an array’s bounds!
