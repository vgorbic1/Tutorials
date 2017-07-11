## Http Request (Firebase Sample) 
Use Google [Firebase](http://firebase.google.com) service to provide backand functionality.

Create a service called `server.service.ts`. (Using CLI: `ng g s server -spec false`)
Make sure you add `ServerService` and `HttpModule` to `app.module.ts` and provide Angular `Http` service to this new service:
```javascript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';

@Injectable()
export class ServerService {
  constructor(private http: Http) { }
}
```
Provide a `storeServer()` method (can use any name for it) that will reach out to the remote server.
```javascript
...
  storeServers(servers: any[]) {
    return this.http.post('https://your-project-url.firebaseio.com/data.json', servers);
  }
...
```
Inject the service to the `app.compoent.ts`:
```javascript
import { Component } from '@angular/core';
import { ServerService } from './server.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  servers = [
    {
      name: 'Testserver',
      capacity: 10,
      id: this.generateId()
    },
    {
      name: 'Liveserver',
      capacity: 100,
      id: this.generateId()
    }
  ];

  constructor(private serverService: ServerService) {}
  onAddServer(name: string) {
    this.servers.push({
      name: name,
      capacity: 50,
      id: this.generateId()
    });
  }
  private generateId() {
    return Math.round(Math.random() * 10000);
  }
}
```
Let's add a button to `app.component.html` that allows us to save data ("Save Servers"):
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <input type="text" #serverName>
      <button class="btn btn-primary" (click)="onAddServer(serverName.value)">Add Server</button>
      <br><br>
      <button class="btn btn-info" (click)="onSave()">Save Servers</button>
      <hr>
      <ul class="list-group" *ngFor="let server of servers">
        <li class="list-group-item">{{ server.name }} (ID: {{ server.id }})</li>
      </ul>
    </div>
  </div>
</div>
```
Create a method to `app.component.ts` to respond to the button click:
```javascript
...
  onSave() {
    this.serverService.storeServers(this.servers)
      .subscribe(
        (response) => console.log(response),
        (error) => console.log(error)
      );
  }
...
```
Run the application and check that your database receives data.
