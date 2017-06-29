## Forms
There are two approaches to handle the form:
- Template-Driven (Angular infers the Form Object from the DOM)
- Reactive (Form is created programmatically and synchronized with the DOM)

### Template-Driven
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
