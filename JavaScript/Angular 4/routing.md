## Routing
Routing provides "multi-page" structure for the application. Put a routes array constant to the `app.module.ts'. The type should be 
`Routes`. Import the class `Routes` from `@angular/router`. Each route is just an object in this arrey. Add new element to
the `imports` array of `@NgModules` called `RouterModule`. Import the "RouterModule` class. Make sure that the `RouterModule` has
a method `forRoot()` that registeres the constant that was created in the beginning.

app.module.ts
```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { Routes, RouterModule } from '@angular/router';  // import Routers and RouterModule 

import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { UsersComponent } from './users/users.component';
import { ServersComponent } from './servers/servers.component';
import { UserComponent } from './users/user/user.component';
import { EditServerComponent } from './servers/edit-server/edit-server.component';
import { ServerComponent } from './servers/server/server.component';
import { ServersService } from './servers/servers.service';

// Create a constant with routes and correspondig components
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'servers', component: ServersComponent }
]; 

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    UsersComponent,
    ServersComponent,
    UserComponent,
    EditServerComponent,
    ServerComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    RouterModule.forRoot(appRoutes)  // add RouterModule and register the constant created above
  ],
  providers: [ServersService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
Add `<router-outlet>` tags in `app.component.html` Also add `routerLink` directive to the navigation bar.
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <ul class="nav nav-tabs">
        <li role="presentation" routerLinkActive="active"
          [routerLinkActiveOptions]="{exact:true}">
          <a routerLink="/">Home</a>
        </li>
        <li role="presentation" routerLinkActive="active">
          <a routerLink="/servers">Servers</a>
        </li>
        <li role="presentation" routerLinkActive="active">
          <a routerLink="/users">Users</a>
        </li>
      </ul>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```
### Parameters in Path
To add parameters to the path use `:` with a custom parameter name:

app.module.ts
```javascript
  { path: 'users/:id/:name', component: UserComponent },
```
To fetch the path parameter, in the component that needs to reach the parameter put the following:

user.component.ts
```javascript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute, Params } from '@angular/router';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
    this.user = {
      id: this.route.snapshot.params['id'],
      name: this.route.snapshot.params['name']
    };
    // use the following optional code if this component may need to be
    // updated from itself.
    this.route.params
      .subscribe(
        (params: Params) => {
          this.user.id = params['id'];
          this.user.name = params['name'];
        }
      );
  }

}
```
user.component.html
```html
<p>User with ID {{ user.id }} loaded.</p>
<p>User name is {{ user.name }}</p>
```
### Query Parameters
To construct a link `/servers/5/edit?allowEdit=1#loading` with query parameters:
```html
<a [routerLink]="['/servers', 5, 'edit']"
   [queryParams]="{allowEdit: '1'}"
   fragment="loading">LINK</a>
```
To construct the same link programatically:
```html
<button class="btn btn-primary" (click)="onLoadServer(1)">
    Load Server 1</button>
```
Put the following to the corresponding `.component.ts`:
```javascript
...
import { Router } from '@angular/router';
...
  constructor(private router: Router) { }
  
  onLoadServer(id: number) {
    this.router.navigate(['/servers', id, 'edit'], 
      {queryParams: {allowEdit: 1},
      fragment: 'loading'});
  }
...
```
