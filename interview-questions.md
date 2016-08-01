## Job Interview Questions
- [**Java**](https://github.com/vgorbic1/Tutorials/blob/master/Java/interview-questions.md)
- [**JavaScript**](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/interview-questions.md)
- [**PHP**](https://github.com/vgorbic1/Tutorials/blob/master/PHP/interview-questions.md)
- [**SQL**](https://github.com/vgorbic1/Tutorials/blob/master/SQL/interview-questions.md)

#### General Questions
**What are the differences between GET and POST methods in form submitting?**

A GET mostly used to retrieve data, usually through a URL where all parameters are visible. A POST is used for writing data and transfers info within the body of request, instead of URL.

**How can we submit a form without a submit button?**

- Using JavaScript: onClick event on the page triggers a function submit() in the script.
- Using PHP: using a header() function with a parameter location:script.php

**How can we get second of the current time using date function?**
- In PHP: `echo(date('s'));`
- In JavaScript: `var date = new Date();  var secs = date.getSeconds();`

**Can you write a palindrome pseudocode?**
- Set "left" to index the first character (or leftmost).
- Set "right" to index the last character (or rightmost).
- Loop. While left is less than right, compare the "left" with "right". If not equal, return FALSE. Increment left, decrement right.
- Return TRUE.

**Can you write a palindrome testing function in Java?**
```java
public static void main(Sting[] args) {
  String strToTest = "level";
  System.out.println(strToTest + " " + isPalindrome(strToTest));
}

static boolean isPalindrome(String stringToTest) {
  int left = 0;
  int right = stringToTest.length() - 1;
  while (left < right) {
    if (stringToTest.charAt(left) != stringToTest.charAt(right)) {
      return false;
    }
    left ++;
    right --;
  }
  return true;
}
```
**Can you write a palidrom testing function in PHP?**
```php
// PHP has a strrev() function that just reverses the string. It is just a matter of comparint that string with a reverse version.

// Otherwise:
$stringToTest = "level";
$myArray = array();
$myArray = str_split($stringToTest);
$stringLength = sizeof($myArray);
$newString = "";

for ($stringLength; $stringLength >= 0; $stringLength--) {
    $newString .= $myArray[$stringLength];
}

if ($stringToTest == $newString) {
    echo "Output: " . $stringToTest . " is a palindrome";
} else {
    echo "Output: " . $stringToTest . " is not a palindrome";
}
```
