## Strings
In Java, a sequence of characters is represented by the class String. The String class is a regular class, and can be handled as such. However, due to its extensive usage, Java added some convenient features that make handling of strings more intuitive.

Java uses UTF-16 encoding for strings where each character has 2 bytes. Strings are objects!

#### Creating a string:
```java
String myString = new Srting("This is my new string");
 // or simply as a string literal:
String myString = "This is my new string";
```

#### Creating constants or singletons:
```java
String myString1 = "Hello!";
String myString2 = "Hello!";
```
This code will create only one object at the run time that contains "Hello!". To make it two different objects with similar value use a default constructor:
```
String myString1 = new String("Hello!");
String myString2 = new String("Hello!");
```

Strings are immutable. Once created and initialized, a String object cannot me modified. Its value cannot be appended, truncated, or replaced. If you need a modifiable string – use the StringBuffer class.

#### Concatenate strings:
```java
String one = "Good";
String two = "day!";
String three = one + " " + two;
```
In loops use stringBuilder for efficiency:
```java
String[] strings = new String[]{"one", "two", "three", "four", "five" };
StringBuilder temp  = new StringBuilder();
for(String string : strings) {
    temp.append(string);
}
String result = temp.toString();
```

#### Get the length of a string:
```java
String myString = "Hello";
int stringLength = myString.length();
```

#### Extracting a part of the string (substring):
```java
String string1 = "Hello World";
String substring = string1.substring(0,5); // The parameters mean take only "from - including, to - excluding".
``` 
The last character in the string has the index String.length() - 1.

#### Search for substrings:
```java
String myString = "Hello World";
int index = myString.indexOf("World"); // result is 6;
```
The indexOf() method returns the index of where the first character in the first matching substring is found. If the substring is not found within the string, the indexOf() method returns -1

#### Comparing strings
```java
Using equals(). If the strings are equal, the equals() method returns true. If not, it returns false:
String one   = "abc";
String two   = "def";
String three = "abc";
String four  = "ABC";
System.out.println( one.equals(two) ); // returns false
System.out.println( one.equals(three) ); // returns true
System.out.println( one.equals(four) ); // returns false
```
Use equalsIgnoreCase() to compares two strings but ignores the case of the characters.

The ```startsWith()``` and ```endsWith()``` methods check if the String starts with a certain substring. Use a parameter for starting index:
```java
String one = "This is a good day to code";
System.out.println( one.startsWith("This")    ); // returns true
System.out.println( one.startsWith("This", 5) ); // returns false
System.out.println( one.endsWith  ("code")    ); // returns true
System.out.println( one.endsWith  ("shower")  ); // returns false
```
The ```compareTo()``` method compares the String to another String and returns an int telling whether this String is smaller, equal to or larger than the other String. If the String is earlier in sorting order than the other String, compareTo() returns a negative number. If the String is equal in sorting order to the other String, compareTo() returns 0. If the String is after the other String in sorting order, the compareTo() method returns a positive number. The value returned by the compareTo() method is calculated as difference between the numeric values of unequal characters (‘a’ - ‘b’ = -1). If one of the strings reaches its end, the method returns the difference of the length of the strings:
```java
String one   = "abc";
String two   = "def";
String three = "abd";
System.out.println( one.compareTo(two)   ); // returns -3
System.out.println( one.compareTo(three) ); // returns -1
```
The ```compareTo()``` method may not work correctly for Strings in different languages than English. To sort Strings correctly in a specific language, use a Collator.

#### Other string manipulations
The ```trim()``` trims a string object. It removes white space characters at the beginning and end of the string. White space characters include space, tab and new lines:
```java
String text = "  And he ran across the field   ";
String trimmed = text.trim(); // result: "And he ran across the field"
```
The ```trim()``` method can be very useful to trim text typed into input fields by a user.

The ```replace()``` method does not actually replace characters in the existing String. Rather, it returns a new String instance, which is equal to the String instance it was created from, but with the given characters replaced:
```java
String source   = "123abc";
String replaced = source.replace('a', '@'); // replaced value is 123@bc
```

The ```split()``` method splits a String into an array of String objects:
```java
String   source = "A man drove with a car.";
String[] occurrences = source.split("a");
```
the occurrences array would contain the String instances: "A m", "n drove with ", " c", "r."
Use a parameter to define number of elements in array.

The ```charAt()``` gets a particular character:
```java
String theString = "This is a good day to code";
System.out.println( theString.charAt(0) ); // returns T
System.out.println( theString.charAt(3) ); // returns s
```

The ```indexOf()``` searchs for a character in a given string:
```java
String s = “abcbcd”;
int pos;
pos = s.indexOf('g'); // pos=-1 (character ‘g’ not found)
pos = s.indexOf('b',2); // pos=+3 (first ‘b’ after position 2
// is in position 3)
pos = s.lastIndexOf('c'); // pos=+4 (last symbol ‘b’ is in position 4)
```
The ```indexOf()``` can be used to search for a substring:
```java
String s = “abcbcd”;
int pos;
pos = s.indexOf('abd'); // pos = -1 (sub-string ‘abd’ not found)
pos = s.indexOf('bc'); // pos = 1 (sub-string ‘bc’ is in position 1)
```

The ```substring()``` extracts a substring:
```java
String s = "abcdef";
String s1 = s.substring(1,3); // s1 = “bc”
String s2 = s.substring(1); // s2 = “bcdef”
```

The ```toCharArray()``` creates character array from a string:
```java
String s = "abcd";
char[] c = s.toCharArray();  // c[0]=’a’ c[1]=’b’ c[2]=’c’ c[3]=’d’
s.getChars(0, 2, c, 2);  // Copy characters in positions 0, 1 of string s into array c starting from position 2.
         // c[0]=’a’ c[1]=’b’ c[2]=’a’ c[3]=’b’
```

The ```getBytes()``` gets the byte representation or the string:
```java
String theString = "This is a good day to code";
byte[] bytes1 = theString.getBytes();
```

The ```copyValueOf()``` creates a String object from an array of characters. It has the following two formats:
```
static copyValueOf(char[] charArray);
static copyValueOf(char[] charArray, int startPosition, int numberOfElements);
```
```java
char[] c = {‘a’, ‘b’, ‘c’, ‘d’};
String s1 = String.copyValueOf(c); // s1 = “abcd”;
String s2 = String.copyValueOf(c,1,2); // s2 = “bc”;
```

#### Converting
Numbers to Strings:
```java
String intStr = String.valueOf(10);
System.out.println("intStr = " + intStr);
```
Objects to Strings:

The Object class contains a method named ```toString()```. Since all Java classes extends (inherits from) the Object class, all objects have a toString() method:
```java
Integer integer = new Integer(123);
String intStr = integer.toString();
```
Uppercase to Lowercase:
```java
String theString = "This IS a mix of UPPERcase and lowerCASE";
String uppercase = theString.toUpperCase();
String lowercase = theString.toLowerCase();
```

#### String Type Switch
Introduced in Java 7.
```java
String yn;
Switch(yn){
    case ("y"): /* handle case y */ break;
    case ("n"): /* handle case n */ break;
    default: /* something fishy? */ break;
}
```

#### Formatted Strings
```java
System.out.printf("%-15s %15s %n", heading1, heading2);
```
- "%s" Format a string with as many characters as are needed.
- "%15s" Format a string with the specified number of characters, and right-justify.
- "%-15s" Format a string with the specifies number of charactrs, and left-justify.

#### toString()
Implementing toString method in java is done by overriding the Object’s toString method. The java toString() method is used when we need a string representation of an object. It is defined in Object class. This method can be overridden to customize the String representation of the Object. Below is a program showing the use of the Object’s Default toString java method.
```java
class PointCoordinates {

	private int x, y;
	public PointCoordinates(int x, int y) {
		this.x = x;
		this.y = y;
	}
	public int getX() {
		return x;
	}
	public int getY() {
		return y;
	}
}

public class ToStringDemo {

	public static void main(String args[]) {
		PointCoordinates point = new PointCoordinates(10, 10);
		// using the Default Object.toString() Method
		System.out.println("Object toString() method : " + point);
		// implicitly call toString() on object as part of string concatenation
		String s = point + " testing";
		System.out.println(s);
	}
}
```
Result:
```
Object toString() method : PointCoordinates@119c082
PointCoordinates@119c082 testing
```
In the above example when we try printing PointCoordinates object, it internally calls the Object’s toString() method as we have not overridden the java toString() method. Since out example has no toString method, the default one in Object is used. The format of the default toString method of the Object is as shown below.

Class Name, “@”, and the hex version of the object’s hashcode concatenated into a string.
The default hashCode method in Object is typically implemented by converting the memory address of the object into an integer.

Below is an example shown of the same program by Overriding the default Object toString() method. The toString() method must be descriptive and should generally cover all the contents of the object.
```java
class PointCoordinates {

	private int x, y;
	public PointCoordinates(int x, int y) {
		this.x = x;
		this.y = y;
	}
	public int getX() {
		return x;
	}
	public int getY() {
		return y;
	}
	// Custom toString() Method.
	public String toString() {
		return "X=" + x + " " + "Y=" + y;
	}
}

public class ToStringDemo2 {

	public static void main(String args[]) {
		PointCoordinates point = new PointCoordinates(10, 10);
		System.out.println(point);
		String s = point + " testing";
		System.out.println(s);
	}
}
```
Result:
```
X=10 Y=10
X=10 Y=10 testing
```
Taken from [here](http://www.wideskills.com/java-tutorial/java-tostring-method)
