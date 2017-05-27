## ng-content Hook
To pass a block of HTML code to a different component use `ng-content` hook.

app.component.html (was)
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
server-element.component.html (was)
```html
     <div class="panel panel-default">
        <div class="panel-heading">{{ element.name }}</div>
        <div class="panel-body">
          <p>
            <strong *ngIf="element.type === 'server'" style="color: red">{{ element.content }}</strong>
            <em *ngIf="element.type === 'blueprint'">{{ element.content }}</em>
          </p>
        </div>
      </div>
```
app.component.html (became)
```html
<div class="container">
  <app-cockpit 
    (serverCreated)="onServerAdded($event)"
    (blueprintCreated)="onBlueprintAdded($event)"></app-cockpit>
  <hr>
  <div class="row">
    <div class="col-xs-12">
    <app-server-element *ngFor="let serverElement of serverElements" [srvElement]="serverElement">
      <!--everything that is between app-server-element tags will be rendered in the child component
      if the child component will have ng-content tags (which is called ng-content hook) -->
      <p>
        <strong *ngIf="serverElement.type === 'server'" style="color: red">{{ serverElement.content }}</strong>
        <em *ngIf="serverElement.type === 'blueprint'">{{ serverElement.content }}</em>
      </p>
    </app-server-element>
    </div>
  </div>
</div>
```
server-element.component.html (became)
```html
     <div class="panel panel-default">
        <div class="panel-heading">{{ element.name }}</div>
        <div class="panel-body">
          <ng-content></ng-content>
        </div>
      </div>
```
