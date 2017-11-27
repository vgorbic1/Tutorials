## Destructors
Destructors are member functions with the same name as the class, preceded by a tilde character
(~). For example, the destructor for the Rectangle class would be named `~Rectangle`.

Destructors are automatically called when an object is destroyed. In the same way that constructors
set things up when an object is created, destructors perform shutdown procedures
when the object goes out of existence. For example, a common use of destructors is to free
memory that was dynamically allocated by the class object.
```c++
class Demo
{
  public:
    Demo(); // Constructor
    ~Demo(); // Destructor
};

Demo::Demo()
{
 cout << "Welcome to the constructor!\n";
}

Demo::~Demo()
{
 cout << "The destructor is now running.\n";
}

int main()
{
 Demo demoObject; // Define a demo object;
 cout << "This program demonstrates an object\n";
 cout << "with a constructor and destructor.\n";
 return 0;
}
```
In addition to the fact that destructors are automatically called when an object is destroyed,
the following points should be mentioned:
- Like constructors, destructors have no return type.
- Destructors cannot accept arguments, so they never have a parameter list.
```c++
...
  public:
    // Constructor
    ContactInfo(char *n, char *p)
    { // Allocate just enough memory for the name and phone number.
      name = new char[strlen(n) + 1];
      phone = new char[strlen(p) + 1];

      // Copy the name and phone number to the allocated memory.
      strcpy(name, n);
      strcpy(phone, p); }

    // Destructor
    ~ContactInfo()
    { delete [] name;
      delete [] phone; }
...
```
