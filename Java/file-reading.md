####Reading from file
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
