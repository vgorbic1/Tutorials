##External Properties and Profiling (for Email functionality)
- Create an external properties file for production and development environment, as well as a common properties file for both scenarios.
They are *application-dev.properties* and *application-prod.properties* files in a hidden folder in your local file system.
- application-prod.properties:
```
#Spring email properties
spring.mail.host=smtp.gmail.com
spring.mail.username=
spring.mail.password=
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.socketFactory.port=465
spring.mail.properties.mail.smtp.socketFactory.class=javax.net.ssl.SSLSocketFactory
spring.mail.properties.mail.smtp.socketFactory.fallback=false
spring.mail.properties.mail.smtp.starttls.enable=true
spring.mail.properties.mail.smtp.ssl.enable=true
```
- Create tow Java configuration classes for production and development profiles. In *src/main/java.com.appname.config* package create a configuration class and name it DevelopmentConfig:
```java
package com.appname.config;

import com.appname.backend.service.EmailService;
import com.appname.backend.service.MockEmailService;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;
import org.springframework.context.annotation.PropertySource;

@Configuration
@Profile("dev")
@PropertySource("file:///${user.home}/.appname/application-dev.properties")
public class DevelopmentConfig {

    @Bean
    public EmailService emailService() {
        return new MockEmailService();
    }
}
```
In *src/main/java.com.appname.config* package create a configuration class and name it ProductinConfig:
```
package com.devopsbuddy.config;

import com.appname.backend.service.EmailService;
import com.appname.backend.service.SmtpEmailService;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;
import org.springframework.context.annotation.PropertySource;

@Configuration
@Profile("prod")
@PropertySource("file:///${user.home}/.appname/application-prod.properties")
public class ProductionConfig {

    @Bean
    public EmailService emailService() {
        return new SmtpEmailService();
    }
}
```
In Spring *application.properties* add this line for executing *development* profile:
```
spring.profiles.active=dev
```
or change "dev" to "prod" for *production* profile.

- Add Email functionality.
