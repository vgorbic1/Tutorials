## Creating Components

### Create a Header
- Create a subdirectory under the `app` directory and name it *header*. 
- Add `header.component.ts` file into the `header` subdirectory.
- Write the following code in that new file:
```
import { Component } from '@angular/core';

@Component({
    selector: 'app-header',
    templateUrl: './header.component.html'
})
export class HeaderComponent {
}
```
- Create a new file in the same `header` directory and name it `header.component.html`.:
```html
<h1>The Header</h1>
```
- Include the component to the app component `app.component.html`:
```html
<app-header></app-header>
<div class="container">
  <div class="row">
    <div class="col-md-12">
      <h1>App Component</h1>
    </div>
  </div>
</div>
```
-add the component in `app.modules.ts`:
```
import { HeaderComponent } from './header/header.component';
...
  declarations: {
    ...
    Header cComponent
    ...
```
- Check if you can see the new component in the browser.
