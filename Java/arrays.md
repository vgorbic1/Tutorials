## Arrays

Declare an array. It does not instantiate it.
```java
int[] myArray;
String[] myArray;
 // or even:
int myArray[];
```
Instantiate an array of 10 elements:
```java
int[] myArray = new int[10]; 
```
If you know values:
```java
int[] myArray = new int[] {1,3,7,9} ; // Creates an array of four elements with corresponding integer values.
 // or even:
String[] myStringArray = {"one", "three", "seven", "nine"};
```
Assign a value to an element:
```java
myArray[0] = 12;
```
Access an array element:
```java
int firstElement = myArray[0]; 
```
Access the length of an array:
```java
int arrayLength = myArray.length;
```
Iterate through an array using for loop:
```java
// Create an array with 10 elements
int[] myArray = new int[10];
// Assign each element with a value
for (int i=0; i<myArray.length; i++) {
    myArray[i] = i;
}
// Display each element
for (int i=0; i<myArray.length; i++) {
    System.out.println(myArray[i]);
}   
``` 
Iterate through an array using for each loop:
```java
String[] myArray = {"one", "twp", "three");
for (String myString : myArray ) {
    System.out.println(myString);
}
```
Multidimensional arrays:
```java
int[][] myArray = new int[10][20]; // each of 10 array elements has 20 elements in it.
myArray[2][13] = 125; // assign a value to one element of the array
```
Iterating multiple arrays:
```java
int[][] myArray = new int[10][20];
for (int i=0; i<myArray.length; i++) {
    for (int j=0; i<myArray[i].length; j++) {
        System.out.println("i: " + i + " j: " + j);
    }
}
```
Inserting elements into an array. Note that the last element in the array will be deleted!
```java
int[] ints = new int[20];
int insertIndex = 10;
int newValue = 123;
// move elements below insertion point:
for (int i=ints.length-1; i>isnertIndex; i--) {
    ints[i] = ints[i-1];
}
// insert new value:
ints[insertIndex] = newValue;
System.out.println(Arrays.toString(ints));
```
Removing elements from an array. The last element of an array will exist twice.
```java
int[] ints = new int[20];
ints[10] = 123;
int removeIndex = 10;
for (int i=removeIndex; i<ints.length-1; i++){
    ints[i] = ints[i + 1];
}
```
#### The Arrays Class
This class is in java.util.Arrays package. Use import statement to apply that functionality:
```java
import java.util.Arrays;
```
Copying a full array using `Arrays.copyOf` method:
```java
int[] source = new int[10];
for (int i=0; i<source.length; i++){
    source[i] = i;
}
int[] destination = Arrays.copyOf(source, soutce.length); // The second parameter specifies how many elements from the source array to copy.
```
Copying a partial array using Arrays.copyOfRange method:
```java
int[] source = new int[10];
for (int i=0; i<source.length; i++){
    source[i] = i;
}
int[] destination = Arrays.copyOfRange(source, 0, soutce.length); //The second parameter is the first index in the source array to include in the copy. The third parameter is the last index in the source array to include in the copy.
```
Converting arrays of primitive types to Strings with Arrays.toString() method:
```java
int[] myArray = new int[10];
for (int i=0; i<myArray.length; i++) {
    myArray[i] = 10 – i;
}
System.out.println(java.util.Arrays.toString(myArray));
// The result will be a string: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1.
```
Sorting arrays using Arrays.sort() method. It works only with primitive types:
```java
int[] myArray = new int[10];
for (int i=0; i<myArray.length; i++) {
    myArray[i] = 10 – i;
}
java.util.Arrays.sort(myArray);
System.out.println(java.util.Arrays.toString(myArray));
// The result will be a string: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```
Sorting arrays of Objects:
```java
Since Objects do not have any natural sort order, you need to define another object that will determine the order of your Objects. It is called a Comparator and is an interface.
Let’s create a class Employee that will hold objects that we need to sort:
private static class Employee {
    public String name;
    public int employeeId;
    public Employee(String name, int employeeId) {
        this.name = name;
        this.employeeId = employeeId;
    }
} 
```
Let’s sort an array of Employee objects by their name using the `Arrays.sort()` method:
```java
Employee[] employeeArray = new Employee[3];
employeeArray[0] = new Employee(“Xander”, 1);
employeeArray[1] = new Employee(“John”, 1);
employeeArray[2] = new Employee(“Anna”, 2);
java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.name.compareTo(e2.name);
    }
});
for (int i=0; i < employeeArray.length; i++) {
    System.out.println(employeeArray[i].name);
}
```
To sort objects by the natural order of their number variables:
```java
java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.employeeId - e2.employeeId;
    }
});
for(int i=0; i < employeeArray.length; i++) {
    System.out.println(employeeArray[i].name);
}
```
To sort objects by the string type and then by the id:
```java
java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        int nameDiff = e1.name.compareTo(e2.name);
        if(nameDiff != 0) { return nameDiff; }
        return e1.employeeId - e2.employeeId;
    }
});
```
Filling Arrays using Arrays.fill() method. There are different variations to fill the array. Look in to the documentation. This is the simplest:
```java
int[] intArray = new int[3];
Arrays.fill(intArray, 123);
System.out.println(Arrays.toString(intArray));
// Results in 123, 123, 123
```
Searching arrays using Arrays.binarySearch() method. The array must be sorted first. There are different variations to search through an array. Look in to the documentation.
Let’s search for value 6 in the given array:
```java
int[] ints = {0,2,4,6,8,10};
int index = Arrays.binarySearch(ints, 6);
System.out.println(index);
// Results is 3, which is an index of the value 6.
```
Checking if arrays are equal with Arrays.equals() method.
```java
int[] ints1 = {0,2,4,6,8,10};
int[] ints2 = {0,2,4,6,8,10};
int[] ints3 = {10,8,6,4,2,0};
boolean ints1EqualsInts2 = Arrays.equals(ints1, ints2);
boolean ints1EqualsInts3 = Arrays.equals(ints1, ints3);
System.out.println(ints1EqualsInts2);
System.out.println(ints1EqualsInts3);
```
