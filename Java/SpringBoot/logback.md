## Logback in Spring Boot Apps
Loggin levels:
- Trace -> Severely slows down an application and create massive output volumes.
- Debug -> Slows down an application and create large output volumes.
- Info -> Used in production environment
- Warn -> Something non-critical happend and requires attention.
- Error -> Investigate and fix ASAP
- Fatal -> Application is not running. Requires immediate attention.

#### Logging Frameworks
- **Log4j** is the most popular loggin framework and is the oldes.
- Log4j was superseded by **log4j2**, which upports JSON configuration amoung other new features.
- **Logback** is gaining popularity with several nice improvements.

#### Logging API
**Slf4j** is a loggin API, which supports levels. It is already included in Spring Boot in ```spring-boot-starter-web``` and
automatically detects chosen Logging Framework.

#### Steps to plug in Logback
Include Logback dependency to pom.xml:
```xml
		<!-- Logging Dependencies -->
		<dependency>
			<groupId>ch.qos.logback</groupId>
			<artifactId>logback-classic</artifactId>
		</dependency>
```
Add logback config file (logback.xml) to the Resources directory of Spring Boot project ```src/main/resources```. This is a sample configuration file: 
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <contextListener class="ch.qos.logback.classic.jul.LevelChangePropagator">
        <resetJUL>true</resetJUL>
    </contextListener>

    <!-- To enable JMX Management -->
    <jmxConfigurator/>

    <!-- This appender prints to console -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%-4relative [%thread] %-5level %logger{35} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- This appender prints to file -->
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${user.home}/logs/appname/appname.log</file>

        <rollingPolicy class="ch.qos.logback.core.rolling.FixedWindowRollingPolicy">
            <fileNamePattern>${user.home}/logs/appname/appname.%i.log.zip</fileNamePattern>
            <minIndex>1</minIndex>
            <maxIndex>3</maxIndex>
        </rollingPolicy>

        <triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">
            <maxFileSize>5MB</maxFileSize>
        </triggeringPolicy>
        <encoder>
            <pattern>%-4relative [%thread] %-5level %logger{35} - %msg%n</pattern>
        </encoder>
    </appender>

    <logger name="com.appname" level="debug" />
    <logger name="uk.co.jemos.podam" level="warn" />
    <logger name="org.springframework" level="info" />
    <logger name="org.hibernate" level="warn" />
    <logger name="org.hibernate.type.descriptor.sql.BasicBinder" level="warn" />
    <logger name="org.springframework.web" level="info" />
    <logger name="org.springframework.security" level="info" />

    <root level="warn">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
    </root>
</configuration>
```
Create a template in your IDE to automatically declare logger in a class. Name it ```slf4j```.
```java
// STS (Eclipse) template:
private static final org.slf4j.Logger LOG = org.slf4j.LoggerFactory.getLogger(${enclosing_type}.class);
```
Use the logger (sample)
```java
public String getMessage(String messageId) {
  LOG.info("Returning i18n text for messageId {}", messageId); // use logger here
  // this "{}" will be substituted with value of the variable "messageId"
  
  Locale locale = LocaleContextHolder.getLocale();
  return getMessage(messageId, locale);
}
```
