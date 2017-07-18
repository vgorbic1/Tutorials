## Authentication
The server sends a JSON token back to the client in order to keep once authenticated user able to communicate
to the server with future requests. The token is hashed with a certain sectret that only server knows.

### Signup page
Use Angular CLI: 
```
ng g c auth/signup --spec false
```
*signup.component.html*
```html
<div class="row">
<div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
<form (ngSubmit)="onSignup(f)" #f="ngForm">
  <div class="form-group">
    <label for="email">Email</label>
    <input type="email" id="email" name="email" ngModel class="form-control">
  </div>
  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" id="password" name="password" ngModel class="form-control">
  </div>
  <button class="btn btn-primary" type="submit">Sign Up</button>
</form>
</div>
</div>
```
*signup.component.ts*
```javascript
import { Component, OnInit } from '@angular/core';
import { NgForm } from '@angular/forms';

@Component({
  selector: 'app-signup',
  templateUrl: './signup.component.html',
  styleUrls: ['./signup.component.css']
})
export class SignupComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

  onSignup(form: NgForm) {
    const email = form.value.email;
    const password = form.value.password;
  }

}
```
Add the page to the routing.
