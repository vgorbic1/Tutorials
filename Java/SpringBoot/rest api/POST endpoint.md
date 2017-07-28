## Implementing a POST endpoint using Spring MVC (Example)
1. Create a new package `rest`.
2. Create a `ReservationResource` class if it does not exist yet.
3. Crete a new method called `createReservation`:
```java
...
	@RequestMapping(path = "", method = RequestMethod.POST, produces = MediaType.APPLICATION_JSON_UTF8_VALUE, 
			consumes = MediaType.APPLICATION_JSON_UTF8_VALUE)
	public ResponseEntity<ReservateionResponse> createReservation(
			@RequestBody
			ReservationRequest reservationRequest) {
		
		return new ResponseEntity<>(new ReservationResponse(), HttpStatus.CREATED);
	}
...
```
4. Create the `ReservationRequest` class that represents a request body which is sent during the POST. Create a new
package `request` in the `model` package:
```java
package com.gorbich.api.demofullstackappangularspringboot.model.request;

import java.time.LocalDate;

import org.springframework.format.annotation.DateTimeFormat;

public class ReservationRequest {

	private Long id;
	@DateTimeFormat(iso = DateTimeFormat.ISO.DATE)
	private LocalDate checkin;
	@DateTimeFormat(iso = DateTimeFormat.ISO.DATE)
	private LocalDate checkout;

	public ReservationRequest() {
		super();
	}

	
	public ReservationRequest(Long id, LocalDate checkin, LocalDate checkout) {
		super();
		this.id = id;
		this.checkin = checkin;
		this.checkout = checkout;
	}


	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public LocalDate getCheckin() {
		return checkin;
	}

	public void setCheckin(LocalDate checkin) {
		this.checkin = checkin;
	}

	public LocalDate getCheckout() {
		return checkout;
	}

	public void setCheckout(LocalDate checkout) {
		this.checkout = checkout;
	}

}
```
5. Import `ReservationRequest` class into `CreateReservation` class.
6. Update `ApiConfig` class to parse formatted dates:
```java
...
	@Bean
	public ObjectMapper objectMapper() {
		ObjectMapper objectMapper = new ObjectMapper();
		objectMapper.registerModule(new JavaTimeModule());
		return new ObjectMapper();
	}
...
```
