## Array (One-dimensional)
Arrays are the basic storage mechanisms available for a sequence of data. The best thing about arrays is that the elements of an
array are collocated sequentially and can be accessed completely and randomly with single instructions.

Inefficiency of on array lies in its size that has to be determined at the time of declaration. If an array size of 100 slots and
only two slots are filled with data, 98 slots are waisted and no other programs can use those memory slots. 

#### Complexity
access | search | insert | remove 
---|---|---|---
O(1) | O(n) | O(n) | O(n)

** C array declaration **
```java
int[] myArray = {1,3,5,65,23,55,123};
```
All the elements in an array are stored in contiguous memory. This makes it possible to access any
element in a constant amount of time.

**Access an element**
```java
public static void getElement(int[] anIntArray, int index) {
  return anIntArray[index];
}
```

**Traverse (print all one by one)**
```java
public static void printAllElements(int[] anIntArray){
  for(int i = 0; i < anIntArray.length; i++){
    System.out.println(anIntArray[i]);
  }
}
```

**Insert an element**
Based on the requirement, a new element can be added at the beginning, end, or any given index of array.

Insert an element **at the end** of an array.
*Algorithm:*


```java


```






**Shift element to another position:**
```java
public static void insertElementAtIndex(int[] array, int startIndex, int targetIndex){
  int value = array[startIndex];
  if (startIndex == targetIndex) {
    return;
  } else if (startIndex < tarGetIndex) {
    for(int i = startIndex+1; i <= targetIndex; i++) {
      array[i-1] = array[i];
    }
    array[targetIndex]=value;
  } else {
    for(int i = startIndex-1; i >= targetIndex; i--){
      array[i+1] = array[i];
    }
    array[targetIndex] = value;
  }
}
```

**Insert an element:**
```java
public static int [] insertExtraElementAtIndex(int[] array, int index, int value) {
  int [] newArray = new int[array.length+1];
  // First, you copy all the elements before the targeted position as they are in the original array:
  for(int i = 0; i < index; i++) {
    newArray[i] = array[i];
  }
  // Then, the new value must be put in the correct position:
  newArray[index] = value;
  // In the end, copy the rest of the elements in the array by shifting their position by one:
  for (int i = index+1; i < newArray.length; i++) {
    newArray[i]=array[i-1];
  }
  return newArray;
}

// When we have the code ready, appending it would mean just inserting it at the end:
public static int[] appendElement(int[] array, int value) {
  return insertExtraElementAtIndex(array, array.length, value);
}
```
