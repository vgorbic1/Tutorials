## Http Request / GET (Firebase Sample) 
Use Google [Firebase](http://firebase.google.com) service to provide backand functionality.

1. Create a service file and add `getServers()` method:
```javascript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';

@Injectable()
export class ServerService {

  constructor(private http: Http) { }

  getServers() {
    return this.http.get('https://udemy-ng-http-1a6e3.firebaseio.com/data.json')
  }
}
```
2. In a template file create a button to get servers:
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <input type="text" #serverName>
      <button class="btn btn-primary" (click)="onAddServer(serverName.value)">Add Server</button>
      <br><br>
      <button class="btn btn-info" (click)="onGet()">Get Servers</button>
      <hr>
      <ul class="list-group" *ngFor="let server of servers">
        <li class="list-group-item">{{ server.name }} (ID: {{ server.id }})</li>
      </ul>
    </div>
  </div>
</div>
```
3. Add `onGet()` method to the `component.ts` file:
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

  onGet() {
    this.serverService.getServers()
      .subscribe(
        (response) => console.log(response),
        (error) => console.log(error)
      );
  }
  private generateId() {
    return Math.round(Math.random() * 10000);
  }
}
```
3. Unwrap the JASON response to a JavaScript object:
```javascript
import { Response } from '@angular/http';
...
  onGet() {
    this.serverService.getServers()
      .subscribe(
        (response: Response) => {
          const data = response.json();
          console.log(data);
        },
        (error) => console.log(error)
      );
  }
...
```
### Extract Data In Sevice File
1. Make sure you import `rxjs/Rx` library and modify the `getServers()` method:
```javascript
import { Headers, Http, Response } from '@angular/http';
import 'rxjs/RX';
...
  getServers() {
    return this.http.get('https://udemy-ng-http-1a6e3.firebaseio.com/data.json')
      .map(
        (response: Response) => {
          const data = response.json();
          return data;
        }
      )
  }
...
```
2. Modify the `app.component.ts` file's `onGet()` method:
```javascript
...
  onGet() {
    this.serverService.getServers()
      .subscribe(
        (servers: Response) => console.log(servers),
        (error) => console.log(error)
      );
  }
...
```
### Transform Data
1. In the `server.service.ts` update the `onGet()` method to prefix the name of the server with `FETCHED_` string:
```javascript
...
  getServers() {
    return this.http.get('https://udemy-ng-http-1a6e3.firebaseio.com/data.json')
      .map(
        (response: Response) => {
          const data = response.json();
          for (const server of data) {
            server.name = 'FETCHED_' + server.name;
          }
          return data;
        }
      )
  }
...
```
2. Get list of services in the `app.component.ts` modifying `onGet()` method:
```javascript
...
  onGet() {
    this.serverService.getServers()
      .subscribe(
        (servers: any[]) => this.servers = servers,
        (error) => console.log(error)
      );
  }
...
```
