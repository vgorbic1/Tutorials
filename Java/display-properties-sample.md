## Display Properties

```java
import java.io.*;
import java.util.*;

/**
 * @author Vlad
 */
public class DisplayProperties {

    private Properties properties;
    private String propertiesFilePath;

    public void run(String path){
        propertiesFilePath = path;
        loadProperties(path);

        System.out.println("Author: " +  
                properties.getProperty("author"));
        System.out.println("Email : " + 
                properties.getProperty("email"));
    }

    public void loadProperties(String propertiesFilePath)  {
        properties = new Properties();
        try {
            properties.load(this.getClass().getResourceAsStream(propertiesFilePath));
        } catch(IOException ioException) {
            ioException.printStackTrace();
        } catch(Exception exception) {
            exception.printStackTrace();
        }
    }

    public static void main(String[] arguments){
        LabThree demo = new LabThree();
        demo.run(arguments[0]);
    }

}
```
Properties File (just a plain text file):
```
author=Vlad
email=vlad@example.com
```
