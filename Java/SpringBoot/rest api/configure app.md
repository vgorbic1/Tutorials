## Configure Application
Use annotated Java classes for the configuration.
1. Create a package named `config`.
2. Within this package create a new class named `ApiConfig`. 
3. Add `@Configuration` annotation.
4. Add two beans to the class:
- *ObjectMapper* (from Jackson library) - defines how JSON strings in the request body
are deserialized from request in POJOs, which will be used to model our data. 
- *ObjectWriter* (from Jackson library) - defines how we serialize our objects into a JSON string
in the response body.

*ApiConfig.java*
```java
package com.gorbich.testapiproject.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.ObjectWriter;

@Configuration
public class ApiConfig {

	@Bean
	public ObjectMapper objectMapper() {
		return new ObjectMapper();
	}
	
	@Bean
	public ObjectWriter objectWriter(ObjectMapper objectMapper) {
		return objectMapper.writerWithDefaultPrettyPrinter();
	}
}
```
5. In the main application class add two annotations:
- `@EnableAutoConfiguration` - intelegently configures beans that you are likely to need in
your Spring Application Context.
- `@ComponentScan` - enables automatic scan for configuration classes to wire up in your
Spring Application Context.

*TestApiProjectApplication*
```java
package com.gorbich.testapiproject;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;

@SpringBootApplication
@EnableAutoConfiguration
@ComponentScan
public class TestApiProjectApplication {

	public static void main(String[] args) {
		SpringApplication.run(TestApiProjectApplication.class, args);
	}
}
```
6. Save files and test run application. 
