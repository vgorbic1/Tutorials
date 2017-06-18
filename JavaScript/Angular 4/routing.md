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
To retrieve data from the link:
```javascript
...
import { ActivatedRoute } from '@angular/router';
...
  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
    console.log(this.route.snapshot.queryParams);
    console.log(this.route.snapshot.fragment);
    // or even better:
    this.route.queryParams.subscribe();
    this.route.fragment.subscribe();
  }
```
### Nested Routing
To provide nesting routes add children to the `app.module.ts':
```javascript
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'servers', component: ServersComponent, children: [
    { path: ':id', component: ServerComponent},
    { path: ':id/edit', component: EditServerComponent }
  ] }
]; 
```
And add the `<router-outlet></router-outlet>` to the component html template, where this data should be displayed.
### Redirecting and Wildcard
To redirect all links that are incorrect to a not-found page, put this in `app.module.ts`:
```javascript
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
...
  { path: 'not-found', component: PageNotFoundComponent },
  { path: '**', redirectTo: '/not-found'} // should always be the last one!
];
```
In our example, we didn't encounter any issues when we tried to redirect the user. But that's not always the case when adding redirections. By default, Angular matches paths by prefix. That means, that the following route will match both `/recipes`  and just `/` 
```
{ path: '', redirectTo: '/somewhere-else' } 
```
Actually, Angular will give you an error here, because that's a common gotcha: This route will now ALWAYS redirect you! Since the default matching strategy is "prefix", Angular checks if the path you entered in the URL does start with the path specified in the route. Of course every path starts with `''`  (Important: That's no whitespace, it's simply "nothing").

To fix this behavior, you need to change the matching strategy to "full" :
```
{ path: '', redirectTo: '/somewhere-else', pathMatch: 'full' } 
```
Now, you only get redirected, if the full path is `''`  (so only if you got NO other content in your path in this example).
### Outsource Routing
Instead of keeping all routs in the `app.module.ts` file, create another file in the `app` directory called `app-routing.module.ts` and 
place the `routs` constant from the `app.module.ts` file to it. Add all imports and remove `RouterModule.forRoot(appRoutes)` from `app.module.ts`. Finally, import this new module in the `app.module.ts`.

app-routing.module.ts:
```javascript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { HomeComponent } from './home/home.component';
import { UsersComponent } from './users/users.component';
import { ServersComponent } from './servers/servers.component';
import { UserComponent } from './users/user/user.component';
import { EditServerComponent } from './servers/edit-server/edit-server.component';
import { ServerComponent } from './servers/server/server.component';
import { ServersService } from './servers/servers.service';
import { PageNotFoundComponent } from './page-not-found/page-not-found.component';

const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent, children: [
    { path: ':id/:name', component: UserComponent }
  ] },
  { path: 'servers', component: ServersComponent, children: [
    { path: ':id', component: ServerComponent},
    { path: ':id/edit', component: EditServerComponent }
  ] },
    { path: 'not-found', component: PageNotFoundComponent },
    { path: '**', redirectTo: '/not-found'}
];

@NgModule({
    imports: [
        RouterModule.forRoot(appRoutes)
    ],
    exports: [RouterModule]
})
export class AppRoutingModule {

}
```
### Guards (CanActivate)
canActivate feature helps to run arbitrary code before routing or right after it.

Create a service file in `app` directory. Make this service class implement `CanActivate` class of Angular core library. Make sure
you also created the `canActivate()` method with two variables and their imports. The method returns boolean:

auth-guard.service.ts
```javascript
import { CanActivate,
    ActivatedRouteSnapshot,
    RouterStateSnapshot,
    Router
 } from '@angular/router';
import { Observable } from 'rxjs/Observable';
import { Injectable } from '@angular/core';
import { AuthService } from './auth.service';

@Injectable()
export class AuthGuard implements CanActivate {
    constructor(private authService: AuthService, private router: Router) {}
    canActivate(route: ActivatedRouteSnapshot,
        state: RouterStateSnapshot): Observable<boolean> |
        Promise<boolean> | boolean {

        return this.authService.isAuthenticated()
            .then(
                (authenticated: boolean) => {
                    if (authenticated) {
                        return true;
                    } else {
                        this.router.navigate(['/']);
                    }
                }
            );
    }
}
```
auth.service.ts
```javascript
export class AuthService {
    loggedIn = false;

    isAuthenticated() {
        const promise = new Promise(
            (resolve, reject) => {
                setTimeout(() => {
                    resolve(this.loggedIn);
                }, 800);
            }
        );
    return promise;
    }

    login() {
        this.loggedIn = true;
    }

    logout() {
        this.loggedIn = false;
    }
}
```
Define which routes should be protected by this guard with `canActive`:
```javascript
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent, children: [
    { path: ':id/:name', component: UserComponent }
  ] },
  { path: 'servers', canActivate: [AuthGuard], component: ServersComponent, children: [
    { path: ':id', component: ServerComponent},
    { path: ':id/edit', component: EditServerComponent }
  ] },
    { path: 'not-found', component: PageNotFoundComponent },
    { path: '**', redirectTo: '/not-found'}
];
```
and do not foget to put new services into `app.module.ts`:
```
providers: [ServersService, AuthService, AuthGuard],
```
