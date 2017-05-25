## Binding to Custom Property
To provide access to the object between to components we need a custom property binding. For that, the object should have a `@Input()` decorator.

app.component.ts
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  serverElements = [{type: 'server', name: 'Test server', content: 'Just a test!'}];
}
```
app.component.html
```html
<div class="container">
  <app-cockpit></app-cockpit>
  <hr>
  <div class="row">
    <div class="col-xs-12">
    <app-server-element *ngFor="let serverElement of serverElements" [element]="serverElement">
    </app-server-element>
    </div>
  </div>
</div>
```
server-element.component.ts
```javascript
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-server-element',
  templateUrl: './server-element.component.html',
  styleUrls: ['./server-element.component.css']
})
export class ServerElementComponent implements OnInit {
  @Input() element: {type: string, name: string, content: string};
  constructor() { }

  ngOnInit() {
  }

}
```
server-element.html
```html
     <div class="panel panel-default">
        <div class="panel-heading">{{ element.name }}</div>
        <div class="panel-body">
          <p>
            <strong *ngIf="element.type === 'server'" style="color: red">{{ element.content }}</strong>
            <em *ngIf="element.type === 'blueprint'">{{ element.content }}</em>
          </p>
        </div>
      </div>
```
### Asigning a Property Alies
It is possible to change the property name (use an alies) when binding to it:

in sever-element.component.ts replace with an alies:
```javascript
...
  @Input('srvElement') element: {type: string, name: string, content: string};
...
```
in app.component.html replace the property with the alies:
```html
...
  <app-server-element *ngFor="let serverElement of serverElements" [srvElement]="serverElement">
...
```
