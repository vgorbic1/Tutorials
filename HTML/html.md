## HTML5

#### Some tips
Always add a trailing slash to subfolder references:
```
href="google.com/folder/"
```
Otherwise, you generate two requests to the server: first, it will add the slash and second, create a new real request.
