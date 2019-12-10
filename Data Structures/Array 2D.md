## Array (two-dimensional)
A two-dimensional array is really nothing more than just an array of arrays. It is better to think of the two-dimensional array as a 
matrix. A matrix can be thought of as a grid of numbers, arranged in rows and columns. A two-dimensional array can also be used to store objects, which is especially convenient for programming sketches that involve some sort of "grid" or "board."

#### Complexity
access | search | insert | remove 
---|---|---|---
O(1) | O(n<sup>2</sup>) | O(n<sup>2</sup>) | O(n<sup>2</sup>)

**C array declaration**
```java
int[][] myArray = {  {0, 1, 2, 3},
                     {3, 2, 1, 0},
                     {3, 5, 6, 1},
                     {3, 8, 3, 4}  };
```

**Access an element**
```java
public static void getElement(int[][] anIntArray) {
  return anIntArray[row][column];
}
```
**Traverse (print all one by one in a matix)**
```java
public static void printAllElements(int[][] anIntArray){
  for (int i = 0; i < anIntArray.length; i++) {
    for (int j = 0; j < anIntArray[i].length; j++) {
      System.out.print(anIntArray[i][j]);
    }
    System.out.println();
  }
}
```
