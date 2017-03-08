##Contact Form
- Create a Pojo to hold the form information. Name it *FeedbackPojo* and put it under *src/main/java.apname.web.domain.frontend* package:
```
package com.appname.web.domain.frontend;

import java.io.Serializable;

public class FeedbackPojo implements Serializable {
	
	private static final long serialVersionUID = 1L;
	
	private String email;
	private String firstName;
	private String lastName;
	private String feedback;
	
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getFirstName() {
		return firstName;
	}
	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public void setLastName(String lastName) {
		this.lastName = lastName;
	}
	public String getFeedback() {
		return feedback;
	}
	public void setFeedback(String feedback) {
		this.feedback = feedback;
	}
	@Override
	public String toString() {
		return "FeedbackPojo [email=" + email + ", firstName=" + firstName + ", lastName=" + lastName + ", feedback="
				+ feedback + "]";
	}
}
```
When a user requests the contact page, the GET request is initiated and an empty *FeedbackPojo* object is created, it is then set to the Spring Map object and finally the user get redirected to the contact page.

When the user fills out form fields and hits "Submit" button, the browser sends a POST request to the *ContactController* post method and feeds the *FeedbackPojo* with the information.
- Create a *ContactController* class under `controllers` package:
```java
package com.appname.web.controllers;

import com.gorbich.devopsbuddy.backend.service.EmailService;
import com.gorbich.devopsbuddy.web.domain.frontend.FeedbackPojo;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
public class ContactController {

    /** The application logger */
    private static final Logger LOG = LoggerFactory.getLogger(ContactController.class);

    /** The key which identifies the feedback payload in the Model. */
    public static final String FEEDBACK_MODEL_KEY = "feedback";

    /** The Contact Us view name. */
    private static final String CONTACT_US_VIEW_NAME = "contact/contact";

    @Autowired
    private EmailService emailService;

    @RequestMapping(value = "/contact", method = RequestMethod.GET)
    public String contactGet(ModelMap model) {
        FeedbackPojo feedbackPojo = new FeedbackPojo();
        model.addAttribute(ContactController.FEEDBACK_MODEL_KEY, feedbackPojo);
        return ContactController.CONTACT_US_VIEW_NAME;
    }

    @RequestMapping(value = "/contact", method = RequestMethod.POST)
    public String contactPost(@ModelAttribute(FEEDBACK_MODEL_KEY) FeedbackPojo feedback) {
        LOG.debug("Feedback POJO content: {}", feedback);
        return ContactController.CONTACT_US_VIEW_NAME;
    }
}
```
- Create a contact.html template and put a form there:
```html
<form id="contactForm"
  th:action="@{/contact/}"
  th:object="${feedback}"
  method="post"
  class="text-left">
  <div class="form-group">
    <label for="email" th:text="#{form.email}"></label>
    <input type="email" id="email" th:field="*{email}" class="form-control" />
  </div>
  <div class="form-group">
    <label for="firstName" th:text="#{form.firstname}"></label>
    <input type="text" id="firstName" th:field="*{firstName}" class="form-control" />
  </div>	
  <div class="form-group">
    <label for="lastName" th:text="#{form.lastname}"></label>
    <input type="text" id="lastName" th:field="*{lastName}" class="form-control" />
  </div>	
  <div class="form-group">
    <label for="feedback" th:text="#{contact.feedback.form.text}"></label>
    <textarea id="feedback" th:field="*{feedback}" class="form-control"></textarea>
  </div>	
  <div class="form-group">
    <button type="submit" class="btn btn-primary" th:text="#{form.submit}"></button>
  </div>							 						 						 						 
</form>
```
- Put necessary i18n properties for the contact form into the *messages.properties* file.
- Test the form. The information should appear in the console.
