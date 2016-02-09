## Log4J Demo

#### Add log4j to IntelliJ project

- File >> Project Structure >> Global Libraries.
- Click green "+" to add a new library.
- Navigate to the IntelliJ application installation directory >> Contents >> lib and select the log4j.jar.
- log4j.jar is now a global library.
- Create a resources directory. Make sure it is set to "Resources".
- Create a log4j.properties file in the resources directory.
- Add log statements to your program.
- Import log4j in your class import org.apache.log4j.*;
- Instantiate the logger: `private final Logger logger = Logger.getLogger(this.getClass());`.
- Log a test statement `logger.info("Some message you want logged");`.
