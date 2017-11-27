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
