## Creating a New Project

To create a new project with Angular CLI use the following command:
```
ng new projectname
```
The CLI will create all components for the project in the ```projectname``` directory.

- Clean up the ```AppComponenet``` class properties (app.component.ts) 
- Clean up the app.component.html file.

#### Adding Bootstrap CSS framework
Move to the project directory. Using CLI install bootstrap module:
```
npm install --save bootstrap
```
Add files to the .angular-cli.json file:
```
"apps" : [
  {
    ...
    "styles": [
      "../node_modules/bootstrap/dist/css/bootstrap.min.css",
      "styles.css"
     ],
```
Test the bootstrap is working. Add the folowing to the app.component.html:
```html
<div class="container">
  <div class="row">
    <div class="col-md-12">
      <h1>Working!</h1>
    </div>
  </div>
</div>
```
