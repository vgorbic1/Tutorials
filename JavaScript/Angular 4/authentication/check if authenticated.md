## Check If the User is Authenticated.
Create a method that checks if the token is created in *auth.service*:
```javascript
...
  isAuthenticated() {
    return this.token != null;
  }
...
```
Make sure that the template is also adjusted: If the user is not authenticated, show the specific menu item:
```html
...
 <ng-template [ngIf]="!authService.isAuthenticated()">
    <li><a routerLink="/signup">Register</a></li>
    <li><a routerLink="/signin">Login</a></li>
 </ng-template>
 ...
<li class="dropdown" appDropdown *ngIf="authService.isAuthenticated()">
  <a style="cursor: pointer;" class="dropdown-toggle" role="button">Manage <span class="caret"></span></a>
    <ul class="dropdown-menu">
      <li><a style="cursor: pointer;" (click)="onSaveData()">Save Data</a></li>
      <li><a style="cursor: pointer;" (click)="onFetchData()">Fetch Data</a></li>
    </ul>
</li>
...
```
