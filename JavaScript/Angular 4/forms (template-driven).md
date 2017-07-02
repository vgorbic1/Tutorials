## Template-Driven Forms
There are two approaches to handle the form:
- Template-Driven (Angular infers the Form Object from the DOM)
- Reactive (Form is created programmatically and synchronized with the DOM)

Make sure you have `FormsModule` in your `app.module.ts` importerd and includet to the `imports` array. When
Angular sees `<form>` tag in .html template, it creates a JS object that represents that form. However, you
still should register the form controls manually. To do that simply add `ngModule` to the `input` tag of the
control. Make sure that the conltrol also has a `name`:
```html
<input type="text" id="username" class="form-control" name="username" ngModel>
```
To make the form submittable you have to add a `(ngSubmit)=` directctive to your form tag, as well as
a method which will be triggered when the form is subnitted. The method should be placed to the `component.ts` 
file of the corresponding template:

*app.component.html*
```html
      <form (ngSubmit)="onSubmit()">
        <div id="user-data">
          <div class="form-group">
            <label for="username">Username</label>
            <input type="text" id="username" class="form-control"
              ngModel name="username">
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
 ```
 *app.component.ts*
 ```javascript
 import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  suggestUserName() {
    const suggestedName = 'Superuser';
  }

  onSubmit() {
    console.log('Submitted!');
  }
}
```
To get access to the form's JavaScript object:
```html
<form (ngSubmit)="onSubmit(f)" #f="ngForm">
```
and in `.component.ts`:
```javascript
import { NgForm } from '@angular/forms';
...
 onSubmit(form: NgForm) {
   console.log(form);
 }
}
```
You also may have access to the form object using `@ViewChild` decoration:
```html
<form (ngSubmit)="onSubmit()" #f="ngForm">
```
and in `.component.ts`:
```javascript
import { Component, ViewChild } from '@angular/core';
import { NgForm } from '@angular/forms';
...
@ViewChild('f') signupForm: NgForm;
...
 onSubmit() {
   console.log(this.signupForm);
 }
}
```
### Validation
Apply validation by adding necessary directive to the <input> tag:
```html
<input type="email" id="email" class="form-control" ngModel name="email" required email />
```
You can style a form control according to the status of its validation:
```html
 <input type="email" id="email" class="form-control" ngModel name="email" required email #email="ngModel"/>
 <span class="help-block" *ngIf="!email.valid && email.touched">Please enter your email</span>
```
*component.css*
```css
input.ng-invalid.ng-touched {
  border: 1px solid red;
}
```
### Default Values
Use property binding with `ngModel` to set default values:
*component.html*
```html
<label for="secret">Secret Questions</label>
<select id="secret" class="form-control" [ngModel]="defaultQuestion" name="secret" email>
   <option value="pet">Your first Pet?</option>
   <option value="teacher">Your first teacher?</option>
</select>
```
*component.ts*
```javascript
...
export class AppComponent {
  defaultQuestion: string = 'pet';
...
```
Use two-way property binding with `ngModel`:
*component.html*
```html
<div class="form-group">
 <textarea name="qAnswer" rows="3" class="form-control" [(ngModel)]="answer"></textarea>
</div>
<p>Your reply: {{ answer }}</p>
```
*component.ts*
```javascript
...
export class AppComponent {
  answer: string = '';
...
```
### Grouping Controls or Fields
To group controls in one object use `ngModelGroup` directive:
```html
<form>
 <div id="user-data" ngModelGroup="userData" #userData="ngModelGroup">
  <div class="form-group">
...
 <p *ngIf="!userData.valid && userData.touched">User Data is invalid!</p>
...
```
### Radio Buttons
*component.html*
```html
<div class="radio" *ngFor="let gender of genders">
 <label>
   <input type="radio" name="gender" ngModel [value]="gender">
   {{ gender }}
 </label>
</div>
```
*component.ts*
```javascript
...
 genders = ['male', 'female'];
...
```
### Setting a Patching Form Value
If you need to set a particular value (suggested value) into the form field before submission, use `patchValue` method:
```html
<div id="user-data" ngModelGroup="userData" #userData="ngModelGroup">
  <div class="form-group">
    <label for="username">Username</label>
    <input type="text" id="username" class="form-control" ngModel name="username" required />
  </div>
  <button class="btn btn-default" type="button" (click)="suggestUserName()">Suggest an Username</button>
...
```
*component.ts*
```javascript
import { Component, ViewChild } from '@angular/core';
...
export class AppComponent {
  @ViewChild('f') signupForm: NgForm; 
...
  suggestUserName() {
    const suggestedName = 'Superuser';
    this.signupForm.form.patchValue({
      userData: {
        username: suggestedName
      }
    })
  }
...
```
### Access Submitted Values
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <form (ngSubmit)="onSubmit(f)" #f="ngForm">
        <div id="user-data" ngModelGroup="userData" #userData="ngModelGroup">
          <div class="form-group">
            <label for="username">Username</label>
            <input type="text" id="username" class="form-control" ngModel name="username" required />
          </div>
          <div class="form-group">
            <label for="email">Mail</label>
            <input type="email" id="email" class="form-control" ngModel name="email" required email #email="ngModel"/>
              <span class="help-block" *ngIf="!email.valid && email.touched">
                Please enter your email
              </span>
          </div>
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
    </div>
  </div>
  <hr>
  <div class="row" *ngIf="submitted">
    <div class="col-xs-12">
      <h3>Your Data</h3>
      <p>Username: {{ user.username }}</p>
      <p>Email: {{ user.email }}</p>
    </div>
  </div>
</div>
```
*component.ts*
```javascript
import { Component, ViewChild } from '@angular/core';
import { NgForm } from '@angular/forms';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  @ViewChild('f') signupForm: NgForm; 
  user = {
    username: '',
    email: ''
  }
  submitted = false;

  onSubmit(form: NgForm) {
    this.submitted = true;
    this.user.username = this.signupForm.value.userData.username;
    this.user.email = this.signupForm.value.userData.email;
    this.signupForm.reset();
  }
}
```
