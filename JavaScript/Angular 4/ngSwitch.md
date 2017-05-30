## ngSwitch
app.component.ts
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  value = 5;
}
```
app.component.html
```html
    <div [ngSwitch]="value">
      <p *ngSwitchCase="5">Value is 5</p>
      <p *ngSwitchCase="10">Value is 10</p>
      <p *ngSwitchCase="100">Value is 100</p>
      <p *ngSwitchDefault>Value is Default</p>
    </div>
```
