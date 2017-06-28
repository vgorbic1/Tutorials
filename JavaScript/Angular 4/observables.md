## Observables
Observables are various Data Sources, such as user input, events, http requests and so on.

There are two components: observable and observer with a stream timeline of multiple events. Observer is our code.

### Types of data packages:
- Handle Data
- Handle Error
- Handle Comletion

![ang](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/Angular%204/images/ang1.jpg)

Sample of a simple observable handeled by Angular itself (no need to import an extra library):

*app.component.html*
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <a routerLink="/">Home</a>
      <a [routerLink]="['user', 1]">User 1</a>
      <a [routerLink]="['user', 2]">User 2</a>
    </div>
  </div>
  <hr>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```
*user.component.ts*
```javascript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute, Params } from '@angular/router';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  id: number;

  constructor(private route: ActivatedRoute) { }
  
  // Observer
  ngOnInit() {
    this.route.params
      .subscribe(
        (params: Params) => {
          this.id = +params['id'];
        }
      );
  }

}
```
Observable object is in `rxjs` library, so you should import it like this:
```
import { Observable } from 'rxjs/Observable';
```
Sometimes you also need `Rx` library:
```
import 'rxjs/Rx';
```
In this sample each second a new number will be printed to the console:
```javascript
import { Component, OnInit } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import 'rxjs/Rx';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor() { }

  ngOnInit() {
    const myNumbers = Observable.interval(1000);
    myNumbers.subscribe(
      (number: number) => {
        console.log(number);
      }
    );
  }
}
```
