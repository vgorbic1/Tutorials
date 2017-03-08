##Email Service
This email service will have to profiles. One *Mock Email Service* for a development environment, that writes message to console. Another an *SMTP Email Service* for the production environment to send real emails.
- Add Spring Boot Email dependency to the pom.xml file:
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```
Use polymorphism to enable profiling for Email Service. The *Adapter* design pattern is used here.

- Create a EmailService interface and put it to *src/main/java.com.appname.backend.service* package:
```java
package com.appname.backend.service;

import com.appname.web.domain.frontend.FeedbackPojo;
import org.springframework.mail.SimpleMailMessage;

public interface EmailService {

    /**
     * Sends an email with the content in the Feedback Pojo.
     * @param feedbackPojo The feedback Pojo
     */
    public void sendFeedbackEmail(FeedbackPojo feedbackPojo);

    /**
     * Sends an email with the content of the Simple Mail Message object.
     * @param message The object containing the email content
     */
    public void sendGenericEmailMessage(SimpleMailMessage message);
}
```
- Create an abstract class *AbstractEmailService* that implements the interface and put it to the same directory where the interface is located.
```java
package com.appname.backend.service;

import com.appname.web.domain.frontend.FeedbackPojo;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.mail.SimpleMailMessage;

public abstract class AbstractEmailService implements EmailService {

    @Value("${default.to.address}")
    private String defaultToAddress;
    /**
     * Creates a Simple Mail Message from a Feedback Pojo.
     * @param feedback The Feedback pojo
     * @return
     */
    protected SimpleMailMessage prepareSimpleMailMessageFromFeedbackPojo(FeedbackPojo feedback) {
        SimpleMailMessage message = new SimpleMailMessage();
        message.setTo(defaultToAddress);
        message.setFrom(feedback.getEmail());
        message.setSubject("[DevOps Buddy]: Feedback received from " + feedback.getFirstName() + " " + feedback
                .getLastName() + "!");
        message.setText(feedback.getFeedback());
        return message;
    }

    @Override
    public void sendFeedbackEmail(FeedbackPojo feedbackPojo) {
        sendGenericEmailMessage(prepareSimpleMailMessageFromFeedbackPojo(feedbackPojo));
    }
}
```
- Add default.to.address property to the application properties file, and put a default email there:
```
default.to.address=info@example.com
```
- Create *MockEmailService* class that extends *AbstractEmailService* class and put it to the same `service` package:
```java
package com.appname.backend.service;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.mail.SimpleMailMessage;

/**
 * Mock implementation of an email service.
 */
public class MockEmailService extends AbstractEmailService {

    /** The application logger */
    private static final Logger LOG = LoggerFactory.getLogger(MockEmailService.class);

    @Override
    public void sendGenericEmailMessage(SimpleMailMessage message) {
        LOG.debug("Simulating an email service...");
        LOG.info(message.toString());
        LOG.debug("Email sent.");
    }
}
```
- Put the *MockEmailService* bean to the *DevelopmentConfig* class:
```
...
public class DevelopmentConfig {
    @Bean
    public EmailService emailService() {
        return new MockEmailService();
    }
}
```
- Inject *MockEmailService* into *ContactController*:
```java
    @Autowired
    private EmailService emailService;
```
