## Pipes
Pipes are features, build into Angular which allows to tranform output in the template.

For example, you have a property: `username = 'Max'`. You can use this property in your template:
`<p>{{ username }}</p>` It looks like `Max` on the screen. Now, you need to transform the property
to the upper case. You can use a pipe: `<p>{{ username | uppercase }}</p>`. Now it looks like `MAX`.

### Pipes Configuration
To parametrize pipes add a colon:
```
{{ sever.started | date:'fullDate' }}
```
Check official documentation for the [list of available pipes](https://angular.io/api?query=pipe).

### Combine Pipes
Add another pipe to chain several pipes:
```
{{ sever.started | date:'fullDate' | uppercase }}
```

### Creating Custom Pipes
Create a new file an call it `shorten.pipe.ts`.
You may use Angular cli command: `ng g p shorten`.
```javascript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'shorten' })
export class ShortenPipe implements PipeTransform {
    transform(value: any) {
        return value.substr(0, 10); // only 10 charecters long
    }

}
```
Make sure you add the class to `app.module.ts`:
```javascript
import { BrowserModule } from '@angular/platform-browser';
...
import { ShortenPipe } from './shorten.pipe';

@NgModule({
  declarations: [
    AppComponent,
    ShortenPipe
  ],
  imports: [
...
```
Now you can use it in the template:
```
{{ server.name | shorten }}
```
#### Adding Parameters to Custom Pipe
To add a parameter to the pipe, just add another parameter to the `transform()` method in `component.ts`:
```javascript
...
 transform(value: any, limit: number) {
      if (value.length > limit) {
        return value.substr(0, limit) + ' ...';
      }
      return value;
    }
 ...
```
To display the parameter:
```
{{ server.name | shorten:5 }}
```
### Filter Example
*app.component.html*
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <input type="text" [(ngModel)]="filteredStatus">
      <ul class="list-group">
        <li
          class="list-group-item"
          *ngFor="let server of servers | filter:filteredStatus:'status'"
          [ngClass]="getStatusClasses(server)">
          <span
            class="badge">
            {{ server.status }}
          </span>
          <strong>{{ server.name | shorten:5 }}</strong> | 
          {{ server.instanceType | uppercase }} | 
          {{ server.started | date:'fullDate' | uppercase }}
        </li>
      </ul>
    </div>
  </div>
</div>
```
*app.component.ts*
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  servers = [
    {
      instanceType: 'medium',
      name: 'Production Server',
      status: 'stable',
      started: new Date(15, 1, 2017)
    },
    {
      instanceType: 'large',
      name: 'User Database',
      status: 'stable',
      started: new Date(15, 1, 2017)
    },
    {
      instanceType: 'small',
      name: 'Development Server',
      status: 'offline',
      started: new Date(15, 1, 2017)
    },
    {
      instanceType: 'small',
      name: 'Testing Environment Server',
      status: 'stable',
      started: new Date(15, 1, 2017)
    }
  ];
  getStatusClasses(server: {instanceType: string, name: string, status: string, started: Date}) {
    return {
      'list-group-item-success': server.status === 'stable',
      'list-group-item-warning': server.status === 'offline',
      'list-group-item-danger': server.status === 'critical'
    };
  }
}
```
*pipe.ts*
```javascript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  pure: false // recalculate the pipe if anything chages on the template
})
export class FilterPipe implements PipeTransform {

  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0 || filterString === '') {
      return value;
    }

    const resultArray = [];
    for (const item of value) {     
      if (item[propName] === filterString) {
        resultArray.push(item);
      }     
    }
    return resultArray;
  }

}
```

