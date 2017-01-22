##Creating JPA Entity
To create a Java Persistent API entity create a simple class using an IDE. To make it a JPA Entity, add @Entity annotation (javax.persistence.Entity) to the class definition.

Add primary key value of type Long and add @Id annotation (javax.persistence.Id) for JPA. To make it automatically generate primary 
key add @GeneratedValue annotation (javax.persistence.GeneratedValue) to the primary key value.

Add other metadata to the class that you need.

For JPA we need a no-argument constructor. Make it private to discourage use of it.

Provide a more convenient constractor with arguments to populate properties (metadata). No need to set primary key value here, in 
constructor. The Hibernate will create one for us via JPA.

Generate Getters and Setters.
```java
package com.gorbich;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Image {
	@Id
	@GeneratedValue
	private Long id;

	private String name;

	private Image() {
	}

	public Image(String name) {
		this.name = name;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
}
```
