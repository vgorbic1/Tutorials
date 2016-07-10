## Strings
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

Strings are immutable. They cannot be changed once created!

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
String substring = string1.substring(0,5); // The parameters mean take only "from - including, to - excluding". The last character in the string has the index String.length() - 1.
```

#### Search for substrings:
```java
String myString = "Hello World";
int index = myString.indexOf("World"); // result is 6
The indexOf() method returns the index of where the first character in the first matching substring is found. If the substring is not found within the string, the indexOf() method returns -1;
```

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
The ```compareTo()``` method compares the String to another String and returns an int telling whether this String is smaller, equal to or larger than the other String. If the String is earlier in sorting order than the other String, compareTo() returns a negative number. If the String is equal in sorting order to the other String, compareTo() returns 0. If the String is after the other String in sorting order, the compareTo() method returns a positive number:
```java
String one   = "abc";
String two   = "def";
String three = "abd";
System.out.println( one.compareTo(two)   ); // returns -3
System.out.println( one.compareTo(three) ); // returns -1
```
The ```compareTo()``` method may not work correctly for Strings in different languages than English. To sort Strings correctly in a specific language, use a Collator.

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

The ```getBytes()``` gets the byte representation or the string:
```java
String theString = "This is a good day to code";
byte[] bytes1 = theString.getBytes();
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
