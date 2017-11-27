## Separating Class (Specification from Implementation)

- Class declarations are stored in their own header files. A header file that contains a
class declaration is called a *class specification* file. The name of the class specification
file is usually the same as the name of the class, with a *.h* extension. For example, the
Rectangle class would be declared in the file *Rectangle.h*.
- The member function definitions for a class are stored in a separate *.cpp* file called
the *class implementation* file. The file usually has the same name as the class, with
the *.cpp* extension. For example, the Rectangle class’s member functions would be
defined in the file *Rectangle.cpp*.
- Any program that uses the class should `#include` the class’s header file. The class’s
*.cpp* file (that which contains the member function definitions) should be compiled
and linked with the main program. This process can be automated with a *project* or
*make* utility. Integrated development environments such as Visual Studio also provide
the means to create the multi-file projects.

```c++
// Specification file for the Rectangle class.
// Rectangle.h
#ifndef RECTANGLE_H
#define RECTANGLE_H

// Rectangle class declaration.

class Rectangle
{
 private:
 double width;
 double length;
 public:
 void setWidth(double);
 void setLength(double);
 double getWidth() const;
 double getLength() const;
 double getArea() const;
};

#endif
```
The `#ifndef` directive is called an *include guard*. It prevents the header
file from accidentally being included more than once.

![ifndef](https://github.com/vgorbic1/Tutorials/blob/master/C-plus-plus/images/includes.jpg)

```c++
// Implementation file for the Rectangle class.
// Rectangle.cpp
#include "Rectangle.h" // Needed for the Rectangle class
#include <iostream> // Needed for cout
#include <cstdlib> // Needed for the exit function
using namespace std;

//***********************************************************
// setWidth sets the value of the member variable width. *
//***********************************************************
void Rectangle::setWidth(double w)
{
 if (w >= 0)
  width = w;
 else {
  cout << "Invalid width\n";
 exit(EXIT_FAILURE);
 }
}

//***********************************************************
// setLength sets the value of the member variable length. *
//***********************************************************
void Rectangle::setLength(double len)
{
 if (len >= 0)
  length = len;
 else
 {
  cout << "Invalid length\n";
  exit(EXIT_FAILURE);
 }
}

//************************************************************
// getWidth returns the value in the member variable width. *
//************************************************************
double Rectangle::getWidth() const
{
  return width;
}

//**************************************************************
// getLength returns the value in the member variable length. *
//**************************************************************
double Rectangle::getLength() const
{
  return length;
}

//************************************************************
// getArea returns the product of width times length. *
//************************************************************
double Rectangle::getArea() const
{
  return width * length;
}
```
`#include` directive includes the *Rectangle.h* file, which contains the Rectangle class declaration.
Notice that the name of the header file is enclosed in double-quote characters ( " " )
instead of angled brackets (< >). When you are including a C++ system header file, such as
iostream , you enclose the name of the file in angled brackets. This indicates that the file
is located in the compiler’s include file directory.

```c++
// This program uses the Rectangle class, which is declared in
// the Rectangle.h file. The member Rectangle class's member
// functions are defined in the Rectangle.cpp file. This program
// should be compiled with those files in a project.
#include <iostream>
#include "Rectangle.h" // Needed for Rectangle class
using namespace std;

int main()
{
  Rectangle box; // Define an instance of the Rectangle class
  double rectWidth; // Local variable for width
  double rectLength; // Local variable for length

  // Get the rectangle's width and length from the user.
  cout << "This program will calculate the area of a\n";
  cout << "rectangle. What is the width? ";
  cin >> rectWidth;
  cout << "What is the length? ";
  cin >> rectLength;
  
  // Store the width and length of the rectangle in the box object.
  box.setWidth(rectWidth);
  box.setLength(rectLength);

  // Display the rectangle's data.
  cout << "Here is the rectangle's data:\n";
  cout << "Width: " << box.getWidth() << endl;
  cout << "Length: " << box.getLength() << endl;
  cout << "Area: " << box.getArea() << endl;
  return 0;
} 
```

Separating a class into a specification file and an implementation file provides a great deal
of flexibility. First, if you wish to give your class to another programmer, you don’t have to
share all of your source code with that programmer. You can give him or her the specification
file and the compiled object file for the class’s implementation. The other programmer
simply inserts the necessary #include directive into his or her program, compiles it, and
links it with your class’s object file. This prevents the other programmer, who might not
know all the details of your code, from making changes that will introduce bugs.

