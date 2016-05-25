## Exception Handling

Exceptions are used in a program to signal that some error or exceptional situation has occurred, and that it doesn't make sense to continue the program flow until the exception has been handled.

Exceptions are regular Java classes that extends java.lang.Exception, or any of the other built-in exception classes.

If a method needs to be able to throw an exception, it has to declare the exception(s) thrown in the method signature, and then include a throw-statement in the method. You can throw any type of exception from your code, as long as your method signature declares it. You can also make up your own exceptions:
```java
public void divide(int numberToDivide, int numberToDivideBy)
    throws BadNumberException {
        if(numberToDivideBy == 0){
            throw new BadNumberException("Cannot divide by 0");
        }
        return numberToDivide / numberToDivideBy;
}
```
When an exception is thrown the method stops execution right after the "throw" statement. The program resumes execution when the exception is caught somewhere by a "catch" block.

#### Catching the exception
Catching the exception is done using a try-catch block.
```java
public void callDivide(){
    try {
        int result = divide(2,1);
        System.out.println(result);
    } catch (BadNumberException e) {
        //do something clever with the exception
        System.out.println(e.getMessage());
    }
    System.out.println("Division attempt done");
}
```
You don't have to catch exceptions thrown from other methods. If you cannot do anything about the exception where the method throwing it is called, you can just let the method propagate the exception up the call stack to the method that called this method.
```
public void callDivide() throws BadNumberException{
        int result = divide(2,1);
        System.out.println(result);
}
```
If an exception is thrown during a sequence of statements inside a try-catch block, the sequence of statements is interrupted and the flow of control will skip directly to the catch-block. This code can be interrupted by exceptions in several places:
```java    
public void openFile(){
  try {
    // constructor may throw FileNotFoundException
    FileReader reader = new FileReader("someFile");
    int i=0;
    while(i != -1){
    //reader.read() may throw IOException
    i = reader.read();
    System.out.println((char) i );
  }
  reader.close();
  System.out.println("--- File End ---");
  } catch (FileNotFoundException e) {
    //do something clever with the exception
  } catch (IOException e) {
    //do something clever with the exception
  }
}
```
This code is a version of the previous method that throws the exceptions (propagates) instead of catching them:
```
public void openFile() throws IOException {
  FileReader reader = new FileReader("someFile");
  int i=0;
  while(i != -1){
    i = reader.read();
    System.out.println((char) i );
  }
  reader.close();
  System.out.println("--- File End ---");
}
```
If an exception is thrown from the reader.read() method then program execution is halted, and the exception is passed up the call stack to the method that called openFile(). If the calling method has a try-catch block, the exception will be caught there.

You can attach a finally-clause to a try-catch block. The code inside the finally clause will always be executed, even if an exception is thrown from within the try or catch block. If your code has a return statement inside the try or catch block, the code inside the finally-block will get executed before returning from the method. Here is how a finally clause looks:
```java
    public void openFile(){
        FileReader reader = null;
        try {
            reader = new FileReader("someFile");
            int i=0;
            while(i != -1){
                i = reader.read();
                System.out.println((char) i );
            }
        } catch (IOException e) {
            //do something clever with the exception
        } finally {
            if(reader != null){
                try {
                    reader.close();
                } catch (IOException e) {
                    //do something clever with the exception
                }
            }
            System.out.println("--- File End ---");
        }
    }
```
You don't need both a catch and a finally block. You can have one of them or both of them with a try-block, but not none of them. This code doesn't catch the exception but lets it propagate up the call stack. Due to the finally block the code still closes the filer reader even if an exception is thrown.
```java
    public void openFile() throws IOException {
        FileReader reader = null;
        try {
            reader = new FileReader("someFile");
            int i=0;
            while(i != -1){
                i = reader.read();
                System.out.println((char) i );
            }
        } finally {
            if(reader != null){
                try {
                    reader.close();
                } catch (IOException e) {
                    //do something clever with the exception
                }
            }
            System.out.println("--- File End ---");
        }
    }
```
#### TRY WITH RESOURCES
Resource Management With Try-Catch-Finally (Old School Style) Managing resources that need to be explicitly closed is somewhat tedious before Java 7. Look at the following method which reads a file and prints it to the System.out:
```java
private static void printFile() throws IOException {
    InputStream input = null;
    try {
        input = new FileInputStream("file.txt");
        int data = input.read();
        while(data != -1){
            System.out.print((char) data);
            data = input.read();
        }
    } finally {
        if(input != null){
            input.close();
        }
    }
}
```
Resource Management With try-with-resources. In Java 7 you can write the code from the example above using the try-with-resource construct like this:
```java
private static void printFileJava7() throws IOException {
    try(FileInputStream input = new FileInputStream("file.txt")) {
        int data = input.read();
        while(data != -1){
            System.out.print((char) data);
            data = input.read();
        }
    }
}
```
Notice the try-with-resources construct inside the method:
```
try(FileInputStream input = new FileInputStream("file.txt"));
```
When the try block finishes the FileInputStream will be closed automatically. This is possible because FileInputStream implements the Java interface java.lang.AutoCloseable. All classes implementing this interface can be used inside the try-with-resources construct.

You can use multiple resources inside a try-with-resources block and have them all automatically closed:
```java
private static void printFileJava7() throws IOException {
    try(  FileInputStream     input         = new FileInputStream("file.txt");
          BufferedInputStream bufferedInput = new BufferedInputStream(input)
    ) {
        int data = bufferedInput.read();
        while(data != -1){
            System.out.print((char) data);
    data = bufferedInput.read();
        }
    }
}
```
