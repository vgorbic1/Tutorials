## Testing with jUnit
Software unit tests help the developer to verify that the logic of a piece of the program is correct. Running tests automatically helps to identify software regressions introduced by changes in the source code. Having a high test coverage of your code allows you to continue developing features without having to perform lots of manual tests. The code which is tested is typically called the code under test. If you are testing an application, this is called the application under test. 

A **unit test** is a piece of code written by a developer that executes a specific functionality in the code to be tested and asserts a certain behavior or state. The percentage of code which is tested by unit tests is typically called test coverage. Unit tests are not suitable for testing complex user interface or component inteaction. For this you should develop integration tests. Typical unit tests are created in a separate project or separate source folder to keep the test code separate from the real code.

An **integration test** has the target to test the behavior of a component or the integration between a set of components. The term functional test is sometimes used as synonym for integration test. Integration tests check that the whole system works as intended, therefore they are reducing the need for intensive manual tests.

**Performance tests** are used to benchmark software components repeatedly. Their purpose is to ensure that the code under test runs fast enough even if it's under high load.

**State testing** is about validating the result, while **behavior testing** is about testing the behavior of the application under test.

In general it is safe to ignore trivial code as, for example, getter and setter methods which simply assign values to fields. Writing tests for these statements is time consuming and pointless, as you would be testing the Java virtual machine. The JVM itself already has test cases for this and if you are developing end user applications you are safe to assume that a field assignment works in Java. If you start developing tests for an existing code base without any tests, it is good practice to start writing tests for the parts of the application in which most of the errors happened in the past. This way you can focus on the critical parts of your application.

JUnit in version 4.x is a test framework which uses annotations to identify methods that specify a test. A JUnit test is a method contained in a class which is only used for testing. This is called a Test class.

The following code shows a JUnit test. This test assumes that the MyClass class exists and has a multiply(int, init) method.
```java
import static org.junit.Assert.assertEquals;
import org.junit.Test;

public class MyTests {

  @Test
  public void multiplicationOfZeroIntegersShouldReturnZero() {

    // MyClass is tested
    MyClass tester = new MyClass();

    // assert statements
    assertEquals("10 x 0 must be 0", 0, tester.multiply(10, 0));
    assertEquals("0 x 10 must be 0", 0, tester.multiply(0, 10));
    assertEquals("0 x 0 must be 0", 0, tester.multiply(0, 0));
  }

} 
```

#### Test Suite
If you have several test classes, you can combine them into a test suite. Running a test suite will execute all test classes in that suite in the specified order. The following example code shows a test suite which defines that two test classes (MyClassTest and MySecondClassTest) should be executed. If you want to add another test class you can add it to @Suite.SuiteClasses statement.
```java
package com.vogella.junit.first;

import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({ MyClassTest.class, MySecondClassTest.class })
public class AllTests {

} 
```
A test suite can also contain other test suites. 

#### Run Tests
The following class demonstrates how to run the MyClassTest. This class will execute your test class and write potential failures to the console, you only need to add the JUnit library JAR file to the classpath.
```java
package de.vogella.junit.first;

import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class MyTestRunner {
  public static void main(String[] args) {
    Result result = JUnitCore.runClasses(MyClassTest.class);
    for (Failure failure : result.getFailures()) {
      System.out.println(failure.toString());
    }
  }
} 
```

#### jUnit annotations
- **@Test** identifies a method as a test method.
- **@Test (expected = Exception.class)**	fails if the method does not throw the named exception.
- **@Test (timeout=100)**	fails if the method takes longer than 100 milliseconds.
- **@Before** executed before each test. It is used to prepare the test environment (e.g., read input data, initialize the class).
- **@After** executed after each test. It is used to cleanup the test environment (e.g., delete temporary data, restore defaults). It can also save memory by cleaning up expensive memory structures.
- **@BeforeClass** executed once, before the start of all tests. It is used to perform time intensive activities, for example, to connect to a database. Methods marked with this annotation need to be defined as static to work with JUnit.
- **@AfterClass** executed once, after all tests have been finished. It is used to perform clean-up activities, for example, to disconnect from a database. Methods annotated with this annotation need to be defined as static to work with JUnit.
- **@Ignore** or **@Ignore ("Why disabled")**	ignores the test method. This is useful when the underlying code has been changed and the test case has not yet been adapted. Or if the execution time of this test is too long to be included. It is best practice to provide the optional description, why the test is disabled.

#### Assert Statements
JUnit provides static methods in the Assert class to test for certain conditions. These assert statements typically start with assert and allow you to specify the error message, the expected and the actual result. An assertion method compares the actual value returned by a test to the expected value, and throws an AssertionException if the comparison test fails.
- **fail(message)**	Let the method fail. Might be used to check that a certain part of the code is not reached or to have a failing test before the test code is implemented. The message parameter is optional.
- **assertTrue([message,] boolean condition)**	Checks that the boolean condition is true. ( [] - means optional )
- **assertFalse([message,] boolean condition)**	Checks that the boolean condition is false.
- **assertEquals([message,] expected, actual)**	Tests that two values are the same. Note: for arrays the reference is checked not the content of the arrays.
- **assertEquals([message,] expected, actual, tolerance)**	Test that float or double values match. The tolerance is the number of decimals which must be the same.
- **assertNull([message,] object)**	Checks that the object is null.
- **assertNotNull([message,] object)**	Checks that the object is not null.
- **assertSame([message,] expected, actual)**	Checks that both variables refer to the same object.
- **assertNotSame([message,] expected, actual)**	Checks that both variables refer to different objects.
JUnit assumes that all test methods can be executed in an arbitrary order. Well-written test code should not assume any order, i.e., tests should not depend on other tests.









