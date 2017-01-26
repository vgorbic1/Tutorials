## Hello World App
A simplie test app that just prints "Hello, World!" in a browser window. Only use Web dependencies. No need for creating a new class. 
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@SpringBootApplication
public class Application {

	@RequestMapping("/")
	String home() {
		return "<h1>Hello, World!</h1>";
	}
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
```
