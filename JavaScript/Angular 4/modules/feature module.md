## Feature Module
Feature module combines several components under one common feature.

![feature](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/Angular%204/images/fm.jpg)

*recipe.module.ts*
```javascript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { RecipesComponent } from './recipes.component';
import ...

@NgModule(
    {
        declarations: [
            RecipesComponent,
            ...
            
        ],
        imports: [
            CommonModule,
            ReactiveFormsModule,
            ...
        ]
    })
export class RecipesModule {

}
```
Make sure you add `CommonModule` to the `imports:` property.
