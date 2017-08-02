## Deployment Steps
1. Set the correct <base> element. If you are runnging you app not from the root domain, for example
`example.com/my-app` you should have
```html
<base href="/my-app/">
```
2. Build your App for Production. Consider Ahead-of-Time Compilation with CLI:
```
ng build --prod --aot
```
3. Make sure your Server ALWAYS returns index.html. Routers are registered in Angular App, so the server
won't know your routes. Return index.html in case of 404 errors.
4. Upload files in your project's `/dist` folder to the root directory of any webserver.
5. Access the url of the server.
