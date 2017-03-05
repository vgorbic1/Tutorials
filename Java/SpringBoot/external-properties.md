##External Properties and Profiling
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
- Create tow Java configuration classes for production and development profiles.
