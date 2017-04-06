## Reading from file
#### Classic Buffer Reader
```java
public void run(String inputFileName) {
    // variable to hold BufferedReader
    BufferedReader = null;
    try {
        input = new BufferedReader(new FileReader("file.txt"));
        // variable to hold each line of the file
        String line = null;
        // loop through all lines in the file
        while (input.ready()) {
            // read each line in file
            line = inputReader.readLine();
            // now process the line in some way
            // this will usually be in another method that
            // we pass the line to.
        }
    // catch all exceptions
    } catch (FileNotFoundException fileNotFound) {
        fileNotFound.printStackTrace();
    } catch (IOException ioException) {
        ioException.printStackTrace();
    } catch (Exception exception) {
        exception.printStackTrace();
    } finally {
        try {
            // if no lines to read – close the file
            if (input != null) {
                input.close();
            }
        } catch (Exception exception) {
            exception.printStackTrace();
        }
    }  
}
```
#### JDK7 
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadFileExample2 {

	private static final String FILENAME = "E:\\test\\filename.txt";

	public static void main(String[] args) {

		try (BufferedReader br = new BufferedReader(new FileReader(FILENAME))) {

			String sCurrentLine;

			while ((sCurrentLine = br.readLine()) != null) {
				System.out.println(sCurrentLine);
			}

		} catch (IOException e) {
			e.printStackTrace();
		}

	}
}
```
or
```java
try(FileInputStream inputStream = new FileInputStream("foo.txt")) {     
    String everything = IOUtils.toString(inputStream);
    // do something with everything string
}
```
