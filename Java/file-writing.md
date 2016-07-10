## Write to File
Write an array to file:
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
