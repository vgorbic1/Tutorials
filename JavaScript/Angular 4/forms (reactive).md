## Reactive Forms
There are two approaches to handle the form:
- Template-Driven (Angular infers the Form Object from the DOM)
- Reactive (Form is created programmatically and synchronized with the DOM)

In reactive approach the form is created programmatically. 
Make sure you have imported `ReactiveFormsModule` instead of `FormsModule` into the `imports:` of your `app.module.ts`.

Use your *component.ts* file to create a property of type `FormGroup`:
```javascript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl } from '@angular/forms';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  genders = ['male', 'female'];
  signupForm: FormGroup;

  ngOnInit() {
    this.signupForm = new FormGroup({
      'username' : new FormControl(null),
      'email' : new FormControl(null),
      'gender' : new FormControl('male')
    });
  }
}
```
*component.html*
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <form [formGroup]="signupForm">
        <div class="form-group">
          <label for="username">Username</label>
          <input
            type="text"
            id="username"
            formControlName="username"
            class="form-control">
        </div>
        <div class="form-group">
          <label for="email">email</label>
          <input
            type="text"
            id="email"
            formControlName="email"
            class="form-control">
        </div>
        <div class="radio" *ngFor="let gender of genders">
          <label>
            <input
              type="radio"
              formControlName="gender"            
              [value]="gender">{{ gender }}
          </label>
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
    </div>
  </div>
</div>
```
### Submitting the Form
```javascript
...
  ngOnInit() {
    this.signupForm = new FormGroup({
      'username' : new FormControl(null),
      'email' : new FormControl(null),
      'gender' : new FormControl('male')
    });
  }

  onSubmit() {
    console.log(this.signupForm);
  }
```
*component.html*
```html
...
<form [formGroup]="signupForm" (ngSubmit)="onSubmit()">
...
```
### Validation
To add validation import `Validators` class to the `component.ts` and apply different validation via references:
```javascript
import { FormGroup, FormControl, Validators } from '@angular/forms';
...
 ngOnInit() {
    this.signupForm = new FormGroup({
      'username' : new FormControl(null, Validators.required),
      'email' : new FormControl(null, [Validators.required, Validators.email]),
      'gender' : new FormControl('male')
    });
  }
...
```
### Access to Controls
```html
<input type="text" id="username" formControlName="username" class="form-control">
<span *ngIf="!signupForm.get('username').valid && signupForm.get('username').touched" class="help-block">Enter username</span>
```
### Nested Form Group
```javascript
 ngOnInit() {
    this.signupForm = new FormGroup({
      'userData' : new FormGroup({
        'username' : new FormControl(null, Validators.required),
        'email' : new FormControl(null, [Validators.required, Validators.email])
      }),
      'gender' : new FormControl('male')
    });
  }
```
*component.html*
```html
<form [formGroup]="signupForm" (ngSubmit)="onSubmit()">
       <div formGroupName="userData">
        <div class="form-group">
          <label for="username">Username</label>
          <input
            type="text"
            id="username"
            formControlName="username"
            class="form-control">
            <span
              *ngIf="!signupForm.get('userData.username').valid && 
              signupForm.get('userData.username').touched" 
              class="help-block">Enter username</span>
        </div>
        <div class="form-group">
          <label for="email">email</label>
          <input
            type="text"
            id="email"
            formControlName="email"
            class="form-control">
        </div>
       </div>
        <div class="radio" *ngFor="let gender of genders">
          <label>
            <input
              type="radio"
              formControlName="gender"            
              [value]="gender">{{ gender }}
          </label>
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
 ```
