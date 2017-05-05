## Array
Arrays are the basic storage mechanisms available for a sequence of data. The best thing about arrays is that the elements of an
array are collocated sequentially and can be accessed completely and randomly with single instructions.

#### Complexity
access | search | insert | remove 
---|---|---|---
O(1) | O(n) | O(n) | O(n)

All the elements in an array are stored in contiguous memory. This makes it possible to access any
element in a constant amount of time.

Traversail / random access:
```java
public static void printAllElements(int[] anIntArray){
  for(int i = 0; i < anIntArray.length; i++){
    System.out.println(anIntArray[i]);
  }
}
```
Shift element to another position:
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
Inserting an element:
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
