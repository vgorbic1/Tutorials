## Constructors
A constructor is a member function that has the same name as the class. It is automatically
called when the object is created in memory, or instantiated. It is helpful to think of constructors
as initialization routines.
```c++
class Demo
{
  public:
    Demo(); // Constructor
};

Demo::Demo()
{
  cout << "Welcome to the constructor!\n";
}
```
A constructor’s purpose is to
initialize an object’s attributes. Because the constructor executes as soon as the object is
created, it can initialize the object’s data members to valid values before those members
are used by other code. It is a good practice to always write a constructor for every class.
```c++
// Specification file for the Rectangle class
// This version has a constructor.
#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle
{
  private:
    double width;
    double length;
  public:
    Rectangle(); // Constructor
    void setWidth(double);
    void setLength(double);

    double getWidth() const { return width; }
    double getLength() const { return length; }
    double getArea() const { return width * length; }
};
#endif
```
Implementation:
```c++
...
Rectangle::Rectangle()
{
  width = 0.0;
  length = 0.0;
}
...
```
### Passing Arguments to Constructors
A constructor can have parameters and can accept arguments when an
object is created.
```c++
// Specification file for the Rectangle class
// This version has a constructor.
#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle
{
  private:
    double width;
    double length;
  public:
    Rectangle(double, double); // Constructor
    void setWidth(double);
    void setLength(double);

    double getWidth() const { return width; }
    double getLength() const { return length; }
    double getArea() const { return width * length; }
};
#endif
```
Implementation:
```c++
Rectangle::Rectangle(double w, double len)
{
  width = w;
  length = len;
}
```
Object Creating:
```c++
...
Rectangle box(10.0, 12.0);
...
```
Like other functions, constructors may have default arguments:
```c++
// class definition
...
  public:
    Sale(double cost, double rate = 0.05)
    { itemCost = cost;
      taxRate = rate; }
...
```
