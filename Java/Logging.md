## Logging with log4j

log4j is a reliable, fast and flexible logging 
framework (APIs) written in Java, which is distributed 
under the Apache Software License. It views the logging 
process in terms of levels of priorities and offers 
mechanisms to direct logging information to a great variety of 
destinations, such as a database, file, console, UNIX Syslog, etc.

log4j has three main components:
- **loggers**: Responsible for capturing logging information.
- **appenders**: Responsible for publishing logging information to various preferred destinations.
- **layouts**: Responsible for formatting logging information in different styles.

Logging does have its drawbacks also. It can slow down an application. If too verbose, it can cause 
scrolling blindness. To alleviate these concerns, log4j is 
designed to be reliable, fast and extensible.

There are two types of objects available with log4j framework.
- Core Objects: They are required to use the framework.
- Support Objects: They are optional and support core objects to perform additional but important tasks.

#### Core Objects
- **Logger Object (layer)** is responsible for capturing logging information and they are stored in a namespace hierarchy.
- **Layout Object (layer)** provides support to appender objects before publishing logging information.
- **Append Object (layer)** is responsible for publishing logging information to various preferred destinations such as a 
database, file, console, UNIX Syslog, etc.

IMAGE

#### Support Objects
- **Level Object** defines the granularity and priority of any logging information. There are seven levels of logging defined 
within the API: OFF, DEBUG, INFO, ERROR, WARN, FATAL, and ALL.
- **Filter Object** object is used to analyze logging information and make further decisions on whether that information should 
be logged or not. Used by Appender Object, that can have several filters.
- **Object Renderer**  is used by Layout objects to prepare the final logging information.
- **Log Manager** manages the logging framework. It is responsible for reading the initial configuration parameters from a 
system-wide configuration file or a configuration class.

#### Configuration
Configuring log4j involves assigning the Level, defining Appender, and specifying Layout objects in a configuration file.

**log4j.properties** file is a log4j configuration file which keeps properties in key-value pairs. By default, the LogManager 
looks for a file named log4j.properties in the CLASSPATH.

Sample log4j.properties file:
```
# Define the root logger with appender file
log4j.rootLogger = DEBUG, FILE

# Define the file appender
# It writes to a file named log.out located in log directory 
log4j.appender.FILE=org.apache.log4j.FileAppender
log4j.appender.FILE.File=${log}/log.out

# Define the layout for file appender
log4j.appender.FILE.layout=org.apache.log4j.PatternLayout
log4j.appender.FILE.layout.conversionPattern=%m%n
````

#### Using log4j in Java Program
Sample program that initializes and uses the log4j library:
```java
import org.apache.log4j.Logger;

import java.io.*;
import java.sql.SQLException;
import java.util.*;

public class log4jExample{

   /* Get actual class name to be printed on */
   static Logger log = Logger.getLogger(log4jExample.class.getName());
   
   public static void main(String[] args)throws IOException,SQLException{
      log.debug("Hello this is a debug message");
      log.info("Hello this is an info message");
   }
}
```
All the libraries should be available in CLASSPATH and 
your log4j.properties file should be available in PATH. Follow the steps give below −
- Create log4j.properties as shown above.
- Create log4jExample.java as shown above and compile it.
- Execute log4jExample binary to run the program.
```
Hello this is a debug message
Hello this is an info message
```

#### Logging Methods
Logger class provides a variety of methods to handle logging activities. The Logger class does not allow us to instantiate a new Logger instance but it provides two static methods for obtaining a Logger object −
- **public static Logger getRootLogger();** returns the application instance's root logger and it does not have a name.
- **public static Logger getLogger(String name);** The name of the logger can be any string you can pass, usually a class or a package name.
```java
static Logger log = Logger.getLogger(log4jExample.class.getName());
```
Once we obtain an instance of a named logger, we can use several methods of the logger to log messages.
All the levels are defined in the org.apache.log4j.Level class and any of the above mentioned methods can be called as follows:
```java
import org.apache.log4j.Logger;

public class LogClass {
   private static org.apache.log4j.Logger log = Logger.getLogger(LogClass.class);
   
   public static void main(String[] args) {
   
      log.trace("Trace Message!");
      log.debug("Debug Message!");
      log.info("Info Message!");
      log.warn("Warn Message!");
      log.error("Error Message!");
      log.fatal("Fatal Message!");
   }
}
```

#### Logging Levels
| Level | Description |
| --- | --- |
| ALL |	All levels including custom levels |
| DEBUG	| Designates fine-grained informational events that are most useful to debug an application |
| ERROR	| Designates error events that might still allow the application to continue running |
| FATAL	| Designates very severe error events that will presumably lead the application to abort |
| INFO | Designates informational messages that highlight the progress of the application at coarse-grained level |
| OFF |	The highest possible rank and is intended to turn off logging |
| TRACE	| Designates finer-grained informational events than the DEBUG |
| WARN | Designates potentially harmful situations |

To filter all our DEBUG and INFO messages usig `setLevel(Level.X)` to set a desired logging level. It prints 
all the messages except Debug and Info:
```java
import org.apache.log4j.*;

public class LogClass {
   private static org.apache.log4j.Logger log = Logger.getLogger(LogClass.class);
   
   public static void main(String[] args) {
      log.setLevel(Level.WARN);

      log.trace("Trace Message!");
      log.debug("Debug Message!");
      log.info("Info Message!");
      log.warn("Warn Message!");
      log.error("Error Message!");
      log.fatal("Fatal Message!");
   }
}
```
But it is better to use the property file to set the levels:
```
# Define the root logger with appender file
log = /usr/home/log4j
log4j.rootLogger = WARN, FILE

# Define the file appender
log4j.appender.FILE=org.apache.log4j.FileAppender
log4j.appender.FILE.File=${log}/log.out

# Define the layout for file appender
log4j.appender.FILE.layout=org.apache.log4j.PatternLayout
log4j.appender.FILE.layout.conversionPattern=%m%n
```
Now, back to the Java code:
```java
import org.apache.log4j.*;

public class LogClass {

   private static org.apache.log4j.Logger log = Logger.getLogger(LogClass.class);
   
   public static void main(String[] args) {
   
      log.trace("Trace Message!");
      log.debug("Debug Message!");
      log.info("Info Message!");
      log.warn("Warn Message!");
      log.error("Error Message!");
      log.fatal("Fatal Message!");
   }
}
```

#### Log Formatting
All Layout objects receive a LoggingEvent object from the Appender objects. The 
Layout objects then retrieve the message argument from the LoggingEvent and apply 
the appropriate ObjectRenderer to obtain the String representation of the message.
The Layout class is defined as abstract within an application, we never use this 
class directly; instead, we work with its subclasses which are as follows:
- DateLayout
- HTMLLayout
- PatternLayout
- SimpleLayout
- XMLLayout

#### Logging in Files
To write your logging information into a file, you would have to use 
org.apache.log4j.FileAppender.

Following is a sample configuration file log4j.properties for FileAppender:
```
# Define the root logger with appender file
log4j.rootLogger = DEBUG, FILE

# Define the file appender
log4j.appender.FILE=org.apache.log4j.FileAppender

# Set the name of the file
log4j.appender.FILE.File=${log}/log.out

# Set the immediate flush to true (default)
log4j.appender.FILE.ImmediateFlush=true

# Set the threshold to debug mode
log4j.appender.FILE.Threshold=debug

# Set the append to false, overwrite
log4j.appender.FILE.Append=false

# Define the layout for file appender
log4j.appender.FILE.layout=org.apache.log4j.PatternLayout
log4j.appender.FILE.layout.conversionPattern=%m%n
```
You may want to write your log messages into multiple files 
for certain reasons, for example, if the file size reached to a certain threshold.

#### Logging in Database
The log4j API provides the org.apache.log4j.jdbc.JDBCAppender object, which can put logging 
information in a specified database.

**Log Table Configuration**
```sql
CREATE TABLE LOGS
   (USER_ID VARCHAR(20)    NOT NULL,
    DATED   DATE           NOT NULL,
    LOGGER  VARCHAR(50)    NOT NULL,
    LEVEL   VARCHAR(10)    NOT NULL,
    MESSAGE VARCHAR(1000)  NOT NULL
   );
```
A sample configuration file log4j.properties for JDBCAppender which will is be used to log 
messages to a LOGS table.
```
# Define the root logger with appender file
log4j.rootLogger = DEBUG, DB

# Define the DB appender
log4j.appender.DB=org.apache.log4j.jdbc.JDBCAppender

# Set JDBC URL
log4j.appender.DB.URL=jdbc:mysql://localhost/DBNAME

# Set Database Driver
log4j.appender.DB.driver=com.mysql.jdbc.Driver

# Set database user name and password
log4j.appender.DB.user=user_name
log4j.appender.DB.password=password

# Set the SQL statement to be executed.
log4j.appender.DB.sql=INSERT INTO LOGS VALUES('%x','%d','%C','%p','%m')

# Define the layout for file appender
log4j.appender.DB.layout=org.apache.log4j.PatternLayout
```
The following Java class is a very simple example that initializes and 
then uses the Log4J logging library for Java applications:
```java
import org.apache.log4j.Logger;
import java.sql.*;
import java.io.*;
import java.util.*;

public class log4jExample{
   /* Get actual class name to be printed on */
   static Logger log = Logger.getLogger(log4jExample.class.getName());
   
   public static void main(String[] args)throws IOException,SQLException{
      log.debug("Debug");
      log.info("Info");
   }
}
```
