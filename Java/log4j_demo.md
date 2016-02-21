## Log4J Demo

#### Add log4j to IntelliJ project

- File >> Project Structure >> Global Libraries.
- Click green "+" to add a new library.
- Navigate to the IntelliJ application installation directory >> Contents >> lib and select the log4j.jar.
- log4j.jar is now a global library.
- Create a resources directory. Make sure it is marked as "Resources Root". (Mark Directory As >>> Resources Root)
- Create a log4j.properties file in the resources directory. Sample:
```
# Set root logger level to INFO, a console appender and a file appender.
# The hierarchy:
# TRACE - all possible messages will be displayed!
# DEBUG - useful for debugging. All, except trace messages will be displayed.
# INFO - standard level. All warnings, error, and fatal messages will be displayed.
# WARN - warnings, error, and fatal messages will be displayed.
# ERROR - error and fatal messages will be displayed.
# FATAL - fatal messages will be displayed only.
log4j.rootLogger=TRACE, CONSOLE, FILE

# CONSOLE is set to be a ConsoleAppender.
log4j.appender.CONSOLE=org.apache.log4j.ConsoleAppender

# CONSOLE uses PatternLayout.
log4j.appender.CONSOLE.layout=org.apache.log4j.PatternLayout
log4j.appender.CONSOLE.layout.ConversionPattern=%d %-4r [%t] %-5p %c %x - %m%n

# FILE is set to be a FileAppender.
log4j.appender.FILE=org.apache.log4j.FileAppender
# Set a name for your log file, which will be found in the root of the project
log4j.appender.FILE.File=MyLog.log
# log4j.appender.FILE.File=C:\\logging.log
### example of logging into tomEE logs directory for web applications
#log4j.appender.FILE.File=${catalina.home}/logs/DemoWebAppLogs/ServletLog.out

# FILE uses PatternLayout.
log4j.appender.FILE.layout=org.apache.log4j.PatternLayout
log4j.appender.FILE.layout.ConversionPattern=%d %-4r [%t] %-5p %c %x - %m%n
```
- Add log statements to your program.
- Import log4j in your class import org.apache.log4j.*;
- Instantiate the logger: `private final Logger logger = Logger.getLogger(this.getClass());`.
- Log a test statement `logger.info("Some message you want logged");`.
