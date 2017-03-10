##In-memeory Authentication
Add a login functionality to protect certain pages of the website.
- Create a LoginController class and put it to `contorllers` package:
```java
package com.appname.web.controllers;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class LoginController {

	public static final String LOGIN_VIEW_NAME = "user/login";
	
	@RequestMapping("/login")
	public String login() {
		return LOGIN_VIEW_NAME;
	}
}
```
- Create a login.html template and put it to the *user* folder of templates:
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="html://www.thymeleaf.org">
<head th:replace="common/header :: common-header" />

<body>
	<div th:replace="common/navbar :: common-navbar" />
	<div class="container">
	    <div class="row">
            <div class="col-md-6 col-md-offset-3 text-center">
                <!-- a login/logout message -->
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
- Set all necessary properties to the i18n properties file.
- Create a payload.html template of the page that should be password proteted. Put it to the *payload* forlder of templates:
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="html://www.thymeleaf.org">
<head th:replace="common/header :: common-header" />

<body>
	<div th:replace="common/navbar :: common-navbar" />
	<div class="container">
		<div class="row">
			<div class="col-md-12">
				<div class="jumbotron">
					<div class="text-center">
					<h1 th:text="#{payload.h1.text}"></h1>
					<p class="lead" th:text="#{payload.p.lead}" />
					</div>
				</div>
			</div>
		</div>
	</div>
	<div th:replace="common/header :: before-body-scripts" />
</body>
</html>
```
- Set all necessary properties to the i18n properties file.
- Create a PayloadController class and put it to `controllers` package.
```java
package com.appname.web.controllers;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class PayloadController {
	
	public static final String PAYLOAD_VIEW_NAME = "payload/payload";
	
	@RequestMapping("/payload")
	public String payload() {
		return PAYLOAD_VIEW_NAME;
	}

}
```
- Add Spring Boot Security dependency to the pom.xml file:
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-security</artifactId>
</dependency>
 ```
 - Create a new SpringConfiguration class and put it to *config* package.
 ```java
 package com.appname.config;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
	
	/** Public URLs. */
    private static final String[] PUBLIC_MATCHERS = {
            "/webjars/**",
            "/css/**",
            "/js/**",
            "/images/**",
            "/",
            "/about/**",
            "/contact/**",
            "/error/**/*",
    };

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers(PUBLIC_MATCHERS).permitAll()
                .anyRequest().authenticated()
                .and()
                .formLogin().loginPage("/login").defaultSuccessUrl("/payload")
                .failureUrl("/login?error").permitAll()
                .and()
                .logout().permitAll();
    }

    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth
                .inMemoryAuthentication()
                .withUser("user").password("password")
                .roles("USER");
    }
}
```
- Add Thymeleaf extra security dependencies to the pom.xml file:
```xml
<dependency>
  <groupId>org.thymeleaf.extras</groupId>
  <artifactId>thymeleaf-extras-springsecurity4</artifactId>
  <version>2.1.2.RELEASE</version>
</dependency>
 ```
 - Update navigation bar with login/logout functionality:
 ```html
<div class="collapse navbar-collapse">
<ul class="nav navbar-nav">
  <li class="active"><a th:text="#{navbar.home.text}" href="/"></a></li>
  <li><a th:text="#{navbar.about.text}" href="/about"></a></li>
  <li><a th:text="#{navbar.contact.text}" href="/contact"></a></li>
</ul>
<ul class="nav navbar-nav navbar-right">
  <li th:if="${#authorization.expression('!isAuthenticated()')}">
    <a th:href="@{/login}" th:text="#{navbar.login.text}" />
  </li>
  <li th:if="${#authorization.expression('isAuthenticated()')}">
     <form id="f" th:action="@{/logout}" method="post" role="form" class="navbar-form">
       <button type="submit" th:text="#{navbar.logout.text}" class="btn btn-primary" />
     </form>
  </li>
</ul>                
</div><!--/.nav-collapse -->
```
- Set all necessary properties to the i18n properties file.
