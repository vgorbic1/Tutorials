## Display Hader on All Pages
To display a header component as the first section on each page set in router,
put it outside the `Switch`:
```js
...
return (
 <div>
  <Header />
  <Switch>
    <Route exact path='/' component={HomePage} />
    <Route path='/page-one' component={PageOne} />
    <Route path='/page-two' component={PageTwo} />
  </ Switch>
 </div>
)
...
```
This is good to show pop-ups, footers, and other sections that are always present on a page.
