##jUnit
Testing is the process of checking the functionality of the application whether it is working as per requirements and to ensure that at developer level, unit testing comes into picture. Unit testing is the testing of single entity (class or method). Unit testing is very essential to every software company to give a quality product to their customers.

JUnit is a unit testing framework for the Java Programming Language. It is important in the test driven development, and is one of a family of unit testing frameworks collectively known as xUnit. JUnit promotes the idea of "first testing then coding", which emphasis on setting up the test data for a piece of code which can be tested first and then can be implemented. This approach is like "test a little, code a little, test a little, code a little..." which increases programmer productivity and stability of program code that reduces programmer stress and the time spent on debugging.

JUnit is an open source framework which is used for writing & running tests. It provides annotation to identify the test methods. It provides assertions for testing expected results. It provides Test runners for running tests. JUnit tests can be run automatically and they check their own results and provide immediate feedback. There's no need to manually comb through a report of test results. JUnit tests can be organized into test suites containing test cases and even other test suites. Junit shows test progress in a bar that is green if test is going fine and it turns red when a test fails.

A formal written unit test case is characterized by a known input and by an expected output, which is worked out before the test is executed. The known input should test a precondition and the expected output should test a post condition. There must be at least two unit test cases for each requirement: one positive test and one negative test. If a requirement has sub-requirements, each sub-requirement must have at least two test cases as positive and negative. JUnit Framework can be easily integrated with Eclipse, Ant or Maven.

Fixtures is a fixed state of a set of objects used as a baseline for running tests. The purpose of a test fixture is to ensure that there is a well-known and fixed environment in which tests are run so that results are repeatable. It includes:
- ```setUp()``` method which runs before every test invocation.
- ```tearDown()``` method which runs after every test method.

Example:
```java
import junit.framework.*;
public class JavaTest extends TestCase {
   protected int value1, value2;  
   // assigning the values
   protected void setUp(){
      value1=3;
      value2=3;
   }
   // test method to add two values
   public void testAdd(){
      double result= value1 + value2;
      assertTrue(result == 6);
   }
}
```
Test suite means bundle a few unit test cases and run it together. In JUnit, both @RunWith and @Suite annotation are used to run the suite test.

Example:
```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
//JUnit Suite Test
@RunWith(Suite.class)
@Suite.SuiteClasses({ 
   TestJunit1.class ,TestJunit2.class
})
public class JunitTestSuite {
}
import org.junit.Test;
import org.junit.Ignore;
import static org.junit.Assert.assertEquals;
public class TestJunit1 {
   String message = "Robert";	
   MessageUtil messageUtil = new MessageUtil(message);  
   @Test
   public void testPrintMessage() {	
      System.out.println("Inside testPrintMessage()");    
      assertEquals(message, messageUtil.printMessage());     
   }
}
import org.junit.Test;
import org.junit.Ignore;
import static org.junit.Assert.assertEquals;
public class TestJunit2 {
   String message = "Robert";	
   MessageUtil messageUtil = new MessageUtil(message); 
   @Test
   public void testSalutationMessage() {
      System.out.println("Inside testSalutationMessage()");
      message = "Hi!" + "Robert";
      assertEquals(message,messageUtil.salutationMessage());
   }
}
```
Test runner is used for executing the test cases. Here is an example which assumes TestJunit test class already exists.

Example:
```java
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;
public class TestRunner {
   public static void main(String[] args) {
      Result result = JUnitCore.runClasses(TestJunit.class);
      for (Failure failure : result.getFailures()) {
         System.out.println(failure.toString());
      }
      System.out.println(result.wasSuccessful());
   }
}
```
JUnit classes are important classes which is used in writing and testing JUnits. Some of the important classes are: Assert - which contain a set of assert methods; TestCase - which contain a test case defines the fixture to run multiple tests; TestResult which contain methods to collect the results of executing a test case.

#### STEP-BY-STEP PROCESS TO START USING JUNIT
Create a java class to be tested say MessageUtil.java 
```java
public class MessageUtil {
   private String message;
   public MessageUtil(String message){
      this.message = message;
   }
   public String printMessage(){
      System.out.println(message);
      return message;
   }   
}  
```
Create a java test class say TestJunit.java. Add a test method testPrintMessage() to your test class.
Add an Annotaion @Test to method testPrintMessage(). Implement the test condition and check the condition using assertEquals API of Junit.
```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;
public class TestJunit {	
   String message = "Hello World";	
   MessageUtil messageUtil = new MessageUtil(message);
   @Test
   public void testPrintMessage() {
      assertEquals(message, messageUtil.printMessage());
   }
}
```
Create a TestRunner java class. Use runClasses() method of JUnitCore class of JUnit to run test case of above created test class. Get the result of test cases run in Result Object. Get failure(s) using getFailures() methods of Result object. Get Success result using wasSuccessful() methods of Result object.
```java
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;
public class TestRunner {
   public static void main(String[] args) {
      Result result = JUnitCore.runClasses(TestJunit.class);
      for (Failure failure : result.getFailures()) {
         System.out.println(failure.toString());
      }
      System.out.println(result.wasSuccessful());
   }
}  	
```
Compile the MessageUtil, Test case and Test Runner classes.
Verify the output.
