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
*app-routing.module.ts*
```javascript```
...
{ path: 'signup', component: SignupComponent }
...
```
### Use Google Firebase for the Back End
Install Firebase package:
```
npm install --save firebase
```
Configure Firebase SDK in *app.component.ts*:
```javascript
import { Component, OnInit } from '@angular/core';
import * as firebase from 'firebase';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  loadedFeature = 'recipe';

  ngOnInit() {
    firebase.initializeApp({
      apiKey: "AIzaS.............TJrrE9mE",
      authDomain: "ng-recipe-book-9f1b5.firebaseapp.com",
    });
  }

  onNavigate(feature: string) {
    this.loadedFeature = feature;
  }
}
```
Create a new service for authorization called *auth.service.ts*
```javascript
import * as firebase from 'firebase';

export class AuthService {
    signupUser(email: string, password: string) {
        firebase.auth().createUserWithEmailAndPassword(email, password)
            .catch(
                error => console.log(error)
            )
    }
}
```
Inject `AuthService` in *signup.component.ts*. Do not forget to provide it in `app.module.ts`:
```javascript
import { Component, OnInit } from '@angular/core';
import { NgForm } from '@angular/forms';
import { AuthService } from '../auth.service';

@Component({
  selector: 'app-signup',
  templateUrl: './signup.component.html',
  styleUrls: ['./signup.component.css']
})
export class SignupComponent implements OnInit {

  constructor(private authService: AuthService) { }

  ngOnInit() {
  }

  onSignup(form: NgForm) {
    const email = form.value.email;
    const password = form.value.password;
    this.authService.signupUser(email, password);
  }

}
```
