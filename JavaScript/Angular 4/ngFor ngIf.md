## ngFor and ngIf directives 
app.component.ts
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  //numbers = [1, 2, 3, 4, 5];
  oddNumbers = [1,3,5];
  evenNumbers = [2,4];
  onlyOdd = false;
}
```
app.component.html
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12">
      <button
        class="btn btn-primary"
        (click)="onlyOdd = !onlyOdd">Only show odd numbers</button>
      <br><br>
      <ul class="list-group">
        <div *ngIf="onlyOdd">
        <li class="list-group-item"
          *ngFor="let odd of oddNumbers">
          {{ odd }}
        </li>
        </div>
        <div *ngIf="!onlyOdd">
        <li class="list-group-item"
          *ngFor="let even of evenNumbers">
          {{ even }}
        </li>
        </div>
      </ul>
      <ng-template [ngIf]="onlyOdd">
        <p>Only odd</p>
      </ng-template>
    </div>
  </div>
</div>
```
