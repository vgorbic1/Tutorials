## Creating a Login Form
- Add a login link to the navigation bar.
```html
    <ul class="nav navbar-nav navbar-right">
      <li><a th:href="@{/login}" th:text="#{navbar.login}" /></li>
    </ul> 
```
- Create a login controller to handle the login action. Name the class LoginContoller.java and put it to ```controllers`` package.
```java
package com.appname.web.controllers;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class LoginController {
	
  public static final String LOGIN_VIEW_NAME = "user/login";
  
	@RequestMapping("/login")
	public String about() {
		return LOGIN_VIEW_NAME;
	}
}
```
- Create a login page and form. Put the login.html page to the ```templates/user``` foldter.
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="html://www.thymeleaf.org">
<head th:replace="common/header :: common-header" />

<body>
	<div th:replace="common/navbar :: common-navbar" />
	<div class="container">
	    <div class="row">
            <div class="col-md-6 col-md-offset-3 text-center">

                <div th:if="${param.error}" class="alert alert-danger alert-dismissible" role="alert">
                    <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                        <span aria-hidden="true">x</span>
                    </button>
                    <p th:text="#{login.error.message}" />
                </div>
                
                <div th:if="${param.logout}" class="alert alert-success alert-dismissible" role="alert">
                    <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                        <span aria-hidden="true">x</span>
                    </button>
                    <p th:text="#{login.logout.success}" />
                </div>
                
            </div>
        </div>
		<div class="row">
			<div class="col-md-6 col-md-offset-3">
				<div class="well">
					<div class="text-center">
						<h1 th:text="#{login.h1.text}"></h1>
						<p class="lead" th:text="#{login.p.lead}" />
					</div>
					<div class="text-left">
          
						<form id="loginForm"
							th:action="@{/login}"
							method="post">
							<div class="form-group">
								<label for="username" th:text="#{login.username.text}" />
								<input class="form-control" type="text" id="username" name="username" />
							</div>
							<div class="form-group">
								<label for="password" th:text="#{login.password.text}" />
								<input class="form-control" type="password" id="password" name="password" />
							</div>
							<div class="form-group">
								<button type="submit" th:text="#{navbar.login.text}" class="btn btn-primary"/>
							</div>															
						</form>
            
					</div>
				</div>
			</div>
		</div>
	</div>
	<div th:replace="common/header :: before-body-scripts" />
</body>
</html>
```
- Put all i18n messages to the ```messages.properties``` file. 
