## Local Reference
Use a local reference to pass data instead two-way data binding. THe local reference and the event to which it is binded should 
be on the same template:

cockpit.component.html (the old variant is commented out)
```html
<div class="row">
    <div class="col-xs-12">
      <p>Add new Servers or blueprints!</p>
      <label>Server Name</label>
      <!--<input type="text" class="form-control" [(ngModel)]="newServerName">-->
      <input type="text" class="form-control" #serverNameInput />
      <br>
      <!--<button
        class="btn btn-primary"
        (click)="onAddServer()">Add Server</button> -->
      <button
        class="btn btn-primary"
        (click)="onAddServer(serverNameInput)">Add Server</button>
    </div>
  </div>
 ```
 cockpit.component.ts (the old variant is commented out)
 ```javascript
 import { Component, OnInit, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-cockpit',
  templateUrl: './cockpit.component.html',
  styleUrls: ['./cockpit.component.css']
})
export class CockpitComponent implements OnInit {
  @Output() serverCreated = new EventEmitter<{serverName: string, serverContent: string}>();
  @Output() blueprintCreated = new EventEmitter<{serverName: string, serverContent: string}>();
  /* newServerName = ''; */

  constructor() { }

  ngOnInit() { }

  /* onAddServer() {
      this.serverCreated.emit({
        serverName: this.newServerName,
      });
  } */

  onAddServer(nameInput: HTMLInputElement) {
      this.serverCreated.emit({
        serverName: nameInput.value,
      });
  }

}
```
