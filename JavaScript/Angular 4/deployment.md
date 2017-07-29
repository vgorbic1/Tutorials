## Deployment Steps
1. Build your App for Production. Consider Ahead-of-Time Compilation
2. Set the correct <base> element. If you are runnging you app not from the root domain, for example
`example.com/my-app` you should have
```html
<base href="/my-app/">
```
3. Make sure your Server ALWAYS returns index.html. Routers are registered in Angular App, so the server
won't know your routes. Return index.html in case of 404 errors.
