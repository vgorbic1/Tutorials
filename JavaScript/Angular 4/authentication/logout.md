## Log Out Functionality
Add logout method in the *auth.service.ts* class:
```javascript
...
  logout() {
    firebase.auth().signOut();
    this.token = null;
  }
...
```
Create a logout link in the template:
```html
...
<li><a style="cursor: pointer;" (click)="onLogout()" *ngIf="authService.isAuthenticated()">Logout</a></li>
...
```
Make sure you add the `onLogout()` method to the component of this template:
```javascript
...
  onLogout() {
    this.authService.logout();
  }
...
```
