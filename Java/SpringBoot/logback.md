##Logback in Spring Boot Apps
Loggin levels:
- Trace -> Severely slows down an application and create massive output volumes.
- Debug -> Slows down an application and create large output volumes.
- Info -> Used in production environment
- Warn -> Something non-critical happend and requires attention.
- Error -> Investigate and fix ASAP
- Fatal -> Application is not running. Requires immediate attention.

####Logging Frameworks
- **Log4j** is the most popular loggin framework and is the oldes.
- Log4j was superseded by **log4j2**, which upports JSON configuration amoung other new features.
- **Logback** is gaining popularity with several nice improvements.

####Logging API
**Slf4j** is a loggin API, which supports levels. It is already included in Spring Boot in ```spring-boot-starter-web``` and
automatically detects chosen Logging Framework.
