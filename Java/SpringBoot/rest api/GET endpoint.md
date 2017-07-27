## Implementing a GET endpoint using Spring MVC (Example)
1. Create a new package `rest`.
2. Create a class `ReservationResource`. and annotate the class with `@RestController` anotation. This annotation combines
`@Controller` annotation and `@RequestBody` annotation. This is a specialization of the `@Component` annotation that
marks the candidate for Autodetection through Class Path Scanning:
- HTTP requests are intersepted by the DispatcherServlet.
- DispatcherServlet looks for handler mappings in that request.
- DispathcerServlet routs the request to correct RestController method.
3. Add `@RequestMapping` endpoint.
4. Create a public method `getAvailableRooms()`, which returns a `ResponseEntity` containing a `ReservationResponse`.
This method will accept two arguments (query or request parameters) In this case `checkin` and `checkout` of `LocalDate` type.
Add `@RequestParam`annotation to the arguments with the field values. Add `@DateTimeFormat` annotation with the field values.
Return `ReponseEntity` with empty `ReservationResponse` with `HttpStatus` code of `OK`.
5. Add `@RequestMapping` annotation to this method with three fields:
- `path` set to empty.
- `method` set to `RequestMethod.GET`.
- `produced` set to `MediaType.APPLICATION_JSON_UTF8_VALUE`

*ReservationResource.java*
```java
package com.gorbich.testapiproject.rest;

import java.time.LocalDate;

import org.springframework.format.annotation.DateTimeFormat;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("room/reservation/v1")
public class ReservationResource {

	@RequestMapping(path = "", method = RequestMethod.GET, produces = MediaType.APPLICATION_JSON_UTF8_VALUE)
	public ResponseEntity<ResevationResponse> getAvailableRooms(
			@RequestParam(value = "checkin")
			@DateTimeFormat(iso = DateTimeFormat.ISO.DATE)
			LocalDate checkin,
			@RequestParam(value = "checkout")
			@DateTimeFormat(iso = DateTimeFormat.ISO.DATE)		
			LocalDate checkout) {
		return new ResponseEntity<>(new ReservationResponse(), HttpStatus.OK);
	}
}
```
6. Create `ReservationResponse` class in a new `model.response` package.
7. Create variables in the class: id, roomNumber, price, and links. Create getters and setters for each variable.
8. Create a constructor with roomNumber and price as parameters.
9. Create an empty constructor.
*ReservationResponse.java*
```java
package com.gorbich.testapiproject.model.response;

public class ReservationResponse {

	private Long id;
	private Integer roomNumber;
	private Integer price;
	private Links links;

	public ReservationResponse() {
		super();
	}

	public ReservationResponse(Integer roomNumber, Integer price) {
		super();
		this.roomNumber = roomNumber;
		this.price = price;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public Integer getRoomNumber() {
		return roomNumber;
	}

	public void setRoomNumber(Integer roomNumber) {
		this.roomNumber = roomNumber;
	}

	public Integer getPrice() {
		return price;
	}

	public void setPrice(Integer price) {
		this.price = price;
	}

	public Links getLinks() {
		return links;
	}

	public void setLinks(Links links) {
		this.links = links;
	}

}
```
10. Create `Links` class in the `model` package, create a private class member `serf`, and getter with setter for this variable.
*Links.java*
```java
package com.gorbich.testapiproject.model;

public class Links {
	
	private Self self;

	public Self getSelf() {
		return self;
	}

	public void setSelf(Self self) {
		this.self = self;
	}
	
}
```
11. Create a `Self` class in the `model` package, create a private class member `ref`, generate getter with setter for this variable.
*Self.java*
```java
package com.gorbich.testapiproject.model;

public class Self {
	private String ref;

	public String getRef() {
		return ref;
	}

	public void setRef(String ref) {
		this.ref = ref;
	}
	
}
```
12. Import the classes that require each other.
13. Install Jackson Datatype: JSR310 Gradle. (Copy the Gradle configuration links from the repository website and
paste it to `build.gradle` file in *dependencies* section.
14. Build gradle Task.
15. Open `application.properties` file and enter a new property:
```
spring.jackson.serialization.write-dates-as-timestamps=false
```
16. Create a `ResourceConstants` class in the `rest` package. Copy the request mapping from `ReservationResource` class.
Create a constant in this class and put the value that was just copied.
*ResourceConstants.java*
```java
package com.gorbich.api.demofullstackappangularspringboot.rest;

public class ResourceConstants {
	public static final String ROOM_RESERVATION_V1 = "/room/reservation/v1";
}
```
17. Replace this value with the constant in `ReservationResource` class
*ReservationResource*
```java
...
@RestController
@RequestMapping(ResourceConstants.ROOM_RESERVATION_V1)
public class ReservationResource {
...
```
18. Run the application.
19. Test the endpoint in the browser. In the URL field type:
```
http://localhost:8080/room/reservation/v1?checkin=2017-03-18&checkout=2016-03-18
```
You should get empty reservation response in JSON format.
