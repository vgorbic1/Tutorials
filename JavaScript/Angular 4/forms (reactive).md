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
### Dynamically add Controls / Arrays of Form Controls
```html
<div formArrayName="hobbies">
 <h4>Your Hobbies</h4>
 <button class="btn btn-default" type="button" (click)="onAddHobbies()">Add Hobbies</button>
 <div class="form-group" *ngFor="let hobbyControl of signupForm.get('hobbies').controls; let i = index">
  <input type="text" class="form-control" [formControlName]="i" >
 </div>
</div>
```
*component.ts*
```javascript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators, FormArray } from '@angular/forms';
...
  onAddHobbies() {
    const control = new FormControl(null, Validators.required);
    (<FormArray>this.signupForm.get('hobbies')).push(control);
  }
}
```
### Custom Validators
```javascript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators, FormArray } from '@angular/forms';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  genders = ['male', 'female'];
  signupForm: FormGroup;
  forbiddenUsernames = ['Anna', 'Pit'];

  ngOnInit() {
    this.signupForm = new FormGroup({
      'userData' : new FormGroup({
        // add custom validation
        'username' : new FormControl(null, [Validators.required, this.forbiddenNames.bind(this)]),
        'email' : new FormControl(null, [Validators.required, Validators.email])
      }),
      'gender' : new FormControl('male'),
      'hobbies' : new FormArray([])
    });
  }

  onSubmit() {
    console.log(this.signupForm);
  }

  onAddHobbies() {
    const control = new FormControl(null, Validators.required);
    (<FormArray>this.signupForm.get('hobbies')).push(control);
  }

  // custom validation method
  forbiddenNames(control: FormControl): {[s: string]: boolean} {
    if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
      return {'nameIsForbidden': true};  // return this object if not valid
    }
    return null;
  }
}
```
*component.html*
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
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
              class="help-block">
              <span *ngIf="signupForm.get('userData.username').errors['nameIsForbidden']">
                The username is taken</span>
              <span *ngIf="signupForm.get('userData.username').errors['required']">
                The username is required</span></span>
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
        <div formArrayName="hobbies">
          <h4>Your Hobbies</h4>
          <button class="btn btn-default"
          type="button"
          (click)="onAddHobbies()">Add Hobbies</button>
          <div class="form-group" *ngFor="let hobbyControl of signupForm.get('hobbies').controls; let i = index">
            <input type="text" class="form-control" [formControlName]="i" >
          </div>
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
    </div>
  </div>
</div>
```
### Asynchronous Validators
The `forbiddenEmails` mehtod will simulate the reachout to the server for data validation:
```javascript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators, FormArray } from '@angular/forms';
import { Observable } from 'rxjs/Observable';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  genders = ['male', 'female'];
  signupForm: FormGroup;
  forbiddenUsernames = ['Anna', 'Pit'];

  ngOnInit() {
    this.signupForm = new FormGroup({
      'userData' : new FormGroup({
        'username' : new FormControl(null, [Validators.required, this.forbiddenNames.bind(this)]),
        'email' : new FormControl(null, [Validators.required, Validators.email],
        this.forbiddenEmails)
      }),
      'gender' : new FormControl('male'),
      'hobbies' : new FormArray([])
    });
  }

  onSubmit() {
    console.log(this.signupForm);
  }

  onAddHobbies() {
    const control = new FormControl(null, Validators.required);
    (<FormArray>this.signupForm.get('hobbies')).push(control);
  }

  forbiddenNames(control: FormControl): {[s: string]: boolean} {
    if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
      return {'nameIsForbidden': true};
    }
    return null;
  }

  forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
    const promise = new Promise<any>((resolve, reject) => {
      // request simuplation
      setTimeout(() =>{ 
        if (control.value == 'test@test.com') {
          resolve({'emailIsForbidden': true});
        } else {
          resolve(null);
        }
      }, 1500)
    });
    return promise;
  }
}
```
### Prepopulate form with values
```javascript
  ngOnInit() {
    this.signupForm = new FormGroup({
      'userData' : new FormGroup({
        'username' : new FormControl(null, [Validators.required, this.forbiddenNames.bind(this)]),
        'email' : new FormControl(null, [Validators.required, Validators.email],
        this.forbiddenEmails)
      }),
      'gender' : new FormControl('male'),
      'hobbies' : new FormArray([])
    });
    
    // preset default values
    this.signupForm.setValue({
      'userData': {
        'username' : 'Vlad',
        'email' : 'example@site.com',

      },
      'gender' : 'male',
      'hobbies' : []
    });
    
    // preset only specific controls
    this.signupForm.patchValue({
      'userData': {
        'username' : 'Jeff',
        'email' : 'jeff@site.com',

      }
    });
  }
  ```
  ### Resettin the form
  Reset the form after submitting it:
  ```javascript
    onSubmit() {
    console.log(this.signupForm);
    this.signupForm.reset();
  }
  ```
  You can pass a specific object to `reset()` as aparameter to clear a certain control only.
