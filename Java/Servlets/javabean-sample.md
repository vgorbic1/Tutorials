## JavaBean
```java
package com.business;
import java.io.Serializable;

public class User implements Serializable {

  private String firstName;
  private String lastName;
  private String email;
  private boolean active;
  
  public User() {
    firstName = "";
    lastName = "";
    email = "";
    active = true;
  }
  
  public User(String firstName, String lastName, String email, boolean active) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.email = email;
    this.active = active;
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
  
  public String getEmail() {
    return email;
  }
  
  public void setEmail(String email) {
    this.email = email;
  }
  
  public boolean isActive() {
    return active;
  }
  
  public void setActive(boolean active) {
    this.active = active;
  }
  
}
```
