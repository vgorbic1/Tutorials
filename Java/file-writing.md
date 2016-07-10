## Write to File
```java
public void run(String fileName, String message) {
        PrintWriter output = null;
        try {
            output =  new PrintWriter(new BufferedWriter(
                new FileWriter(fileName)));
            output.println(message);
        } catch (IOException ioException) {
            ioException.printStackTrace();
        } catch (Exception excepton) {
            excepton.printStackTrace();
        } finally {
             if (output != null) {
                 output.close();
             }
        }
    }
```
PrintWriter prints characters!

Write an array list to file:
```java
import java.io.*;
import java.util.*;

/**
 * @author Vlad Gorbich
 */
public class WriteArrayToFile {

    private ArrayList<String> list;

    public void run(String outputFilePath) {
        list = new ArrayList<String>();

        list.add("one");
        list.add("two");
        list.add("three");
        list.add("four");
        list.add("five");
        list.add("six");
        list.add("seven");
        list.add("eight");
        list.add("nine");
        list.add("ten");

        writeListToOutputFile(outputFilePath);
    }

    private void writeListToOutputFile(String outputFilePath) {
        PrintWriter output = null;
        try {
            output = new PrintWriter(new BufferedWriter(new 
                              FileWriter(outputFilePath)));

            for (String element : list) {
                output.println(element);
            }

        } catch (IOException ioException) {
            ioException.printStackTrace();
        } catch (Exception exception) {
            exception.printStackTrace();
        } finally {
            if (output != null) {
                output.close();
            }
        }

    }

    public static void main(String[] arguments) {
        if (arguments.length != 1) {
            System.out.println("Please enter one argument on the command line, an output file name");
            return;
        }

        LabSeven labSeven = new LabSeven();
        labSeven.run(arguments[0]);
    }

}
```
Write set to file:
```java
import java.io.*;
import java.util.*;

/**
 * @author Vlad Gorbich
 */
public class WriteSetToFile {

    private Set<String> set;

    public void run(String outputFilePath) {
        set = new TreeSet<String>();

        set.add("one");
        set.add("one");
        set.add("five");
        set.add("two");
        set.add("four");
        set.add("two");
        set.add("three");
        set.add("three");
        set.add("four");
        set.add("three");

        writeSetToOutputFile(outputFilePath);
    }

    private void writeSetToOutputFile(String outputFilePath) {
        PrintWriter output = null;
        try {
            output = new PrintWriter(new BufferedWriter(new FileWriter(outputFilePath)));

            for (String element : set) {
                output.println(element);
            }

        } catch (IOException ioException) {
            ioException.printStackTrace();
        } catch (Exception exception) {
            exception.printStackTrace();
        } finally {
            if (output != null) {
                output.close();
            }
        }

    }

    public static void main(String[] arguments) {
        if (arguments.length != 1) {
            System.out.println("Please enter one argument on the command line, an output file name");
            return;
        }

        LabEight labEight = new LabEight();
        labEight.run(arguments[0]);
    }

}
```
