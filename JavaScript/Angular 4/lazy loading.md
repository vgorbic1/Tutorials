## Lazy Loading
Load modules only when you need them. For example, load a module when a particular route is visited.

### Implementation
Add a `loadChildren` in the `app-routing.module.ts` to the route for the module you want to load lazily:
```javascript
...
  { path: '', component: HomeComponent },
  { path: 'recipes', loadChildren: './recipes/recipe.module#RecipesModule'},
...
```
What if you want to use route protection (canActivate  to be precise) on lazily loaded routes?

You can add canActivate to the lazy loaded routes but that of course means, that you might load code which in the end can't get accessed anyways. It would be better to check that BEFORE loading the code.
You can enforce this behavior by adding the canLoad  guard to the route which points to the lazily loaded module:
```javascript
...
{ path: 'recipes', loadChildren: './recipes/recipes.module#RecipesModule', canLoad: [AuthGuard] } 
...
```

### Preloading
In `app-routin.module.ts` add `preloadingStrategy: PreloadAllModules` property and value. Do not forget
to import `PreloadAllModules` from `@angular/router`:
```javascript
...
@NgModule({
  imports: [RouterModule.forRoot(appRoutes, {preloadingStrategy: PreloadAllModules})],
  exports: [RouterModule]
})
...
```
