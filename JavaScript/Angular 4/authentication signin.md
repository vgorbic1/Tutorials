## Authentication

### Sign In Form
## Authentication
The server sends a JSON token back to the client in order to keep once authenticated user able to communicate
to the server with future requests. The token is hashed with a certain sectret that only server knows.

### Signup page
Use Angular CLI: 
```
ng g c auth/signin --spec false
```
*signin.component.html*
```html
<div class="row">
<div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
<form (ngSubmit)="onSignin(f)" #f="ngForm">
  <div class="form-group">
    <label for="email">Email</label>
    <input type="email" id="email" name="email" ngModel class="form-control">
  </div>
  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" id="password" name="password" ngModel class="form-control">
  </div>
  <button class="btn btn-primary" type="submit">Sign In</button>
</form>
</div>
</div>
```
*signin.component.ts*
```javascript
import { Component, OnInit } from '@angular/core';
import { NgForm } from '@angular/forms';

@Component({
  selector: 'app-signup',
  templateUrl: './signin.component.html',
  styleUrls: ['./signin.component.css']
})
export class SigninComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

  onSignin(form: NgForm) {
    const email = form.value.email;
    const password = form.value.password;
  }

}
```
Add a `signinUser()` method to *auth.service.ts* (look in [authentication signup]() page)
