## Testing with jUnit
Software unit tests help the developer to verify that the logic of a piece of the program is correct. Running tests automatically helps to identify software regressions introduced by changes in the source code. Having a high test coverage of your code allows you to continue developing features without having to perform lots of manual tests. The code which is tested is typically called the code under test. If you are testing an application, this is called the application under test. 

A **unit test** is a piece of code written by a developer that executes a specific functionality in the code to be tested and asserts a certain behavior or state. The percentage of code which is tested by unit tests is typically called test coverage. Unit tests are not suitable for testing complex user interface or component inteaction. For this you should develop integration tests. Typical unit tests are created in a separate project or separate source folder to keep the test code separate from the real code.

An **integration test** has the target to test the behavior of a component or the integration between a set of components. The term functional test is sometimes used as synonym for integration test. Integration tests check that the whole system works as intended, therefore they are reducing the need for intensive manual tests.

**Performance tests** are used to benchmark software components repeatedly. Their purpose is to ensure that the code under test runs fast enough even if it's under high load.

**State testing** is about validating the result, while **behavior testing** is about testing the behavior of the application under test.

In general it is safe to ignore trivial code as, for example, getter and setter methods which simply assign values to fields. Writing tests for these statements is time consuming and pointless, as you would be testing the Java virtual machine. The JVM itself already has test cases for this and if you are developing end user applications you are safe to assume that a field assignment works in Java. If you start developing tests for an existing code base without any tests, it is good practice to start writing tests for the parts of the application in which most of the errors happened in the past. This way you can focus on the critical parts of your application.









