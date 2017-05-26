## Binding to Custom Event
Custom event binding is used to inform a parent (or another) component about event from a child (different) component.

app.component.html
```html
<div class="container">
  <app-cockpit 
    (serverCreated)="onServerAdded($event)"
    (blueprintCreated)="onBlueprintAdded($event)"></app-cockpit>
  <hr>
  <div class="row">
    <div class="col-xs-12">
    <app-server-element *ngFor="let serverElement of serverElements" [srvElement]="serverElement">
    </app-server-element>
    </div>
  </div>
</div>
```
app.component.ts
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  serverElements = [{type: 'server', name: 'Testserver', content: 'Just a test!'}];

  onServerAdded(serverData: {serverName: string, serverContent: string}) {
    this.serverElements.push({
      type: 'server',
      name: serverData.serverName,
      content: serverData.serverContent
    });
  }

  onBlueprintAdded(blueprintData: {serverName: string, serverContent: string}) {
    this.serverElements.push({
      type: 'blueprint',
      name: blueprintData.serverName,
      content: blueprintData.serverContent
    });
  }
}
```
cockpit.component.html
```html
<div class="row">
    <div class="col-xs-12">
      <p>Add new Servers or blueprints!</p>
      <label>Server Name</label>
      <input type="text" class="form-control" [(ngModel)]="newServerName">
      <label>Server Content</label>
      <input type="text" class="form-control" [(ngModel)]="newServerContent">
      <br>
      <button
        class="btn btn-primary"
        (click)="onAddServer()">Add Server</button>
      <button
        class="btn btn-primary"
        (click)="onAddBlueprint()">Add Server Blueprint</button>
    </div>
  </div>
  ```
  cockpit.component.ts
  ```javascript
  @Component({
  selector: 'app-cockpit',
  templateUrl: './cockpit.component.html',
  styleUrls: ['./cockpit.component.css']
})
export class CockpitComponent implements OnInit {
  @Output() serverCreated = new EventEmitter<{serverName: string, serverContent: string}>();
  @Output() blueprintCreated = new EventEmitter<{serverName: string, serverContent: string}>();
  newServerName = '';
  newServerContent = '';

  constructor() { }

  ngOnInit() { }

  onAddServer() {
      this.serverCreated.emit({
        serverName: this.newServerName,
        serverContent: this.newServerContent
      });
  }

  onAddBlueprint() {
      this.blueprintCreated.emit({
        serverName: this.newServerName,
        serverContent: this.newServerContent
      });
  }
}
```
