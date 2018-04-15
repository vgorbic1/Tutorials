## Sample to create an image grid with Flex:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
  html, body {
    background-color: #ffeead;
    margin: 10px;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
  }
  .container > div {
    flex: 1 1 150px;
  }
  .container > div > img {
    border: 1px solid black;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  </style>
</head>
<body>
  <div class="container">
    <div><img src="http://placehold.it/150x100" /></div>
    <div><img src="http://placehold.it/300x200" /></div>
    <div><img src="http://placehold.it/300x200" /></div>
    <div><img src="http://placehold.it/150x100" /></div>
    <div><img src="http://placehold.it/300x200" /></div>
    <div><img src="http://placehold.it/150x100" /></div>
    <div><img src="http://placehold.it/300x200" /></div>
    <div><img src="http://placehold.it/150x100" /></div>
    <div><img src="http://placehold.it/300x200" /></div>
    <div><img src="http://placehold.it/300x200" /></div>
    <div><img src="http://placehold.it/150x100" /></div>    
  </nav>
</body>
</html>
```
Enhanced version:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
  html, body {
    background-color: #ffeead;
    margin: 10px;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
  }
  .container > div > img {
    border: 1px solid black;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .container > .normal {
    flex: 1 1 150px;
  }
  .container > .big {
    flex: 1 1 300px;
  }
  </style>
</head>
<body>
  <div class="container">
    <div class="normal"><img src="http://placehold.it/150x100" /></div>
    <div class="big"><img src="http://placehold.it/300x200" /></div>
    <div class="big"><img src="http://placehold.it/300x200" /></div>
    <div class="normal"><img src="http://placehold.it/150x100" /></div>
    <div class="big"><img src="http://placehold.it/300x200" /></div>
    <div class="normal"><img src="http://placehold.it/150x100" /></div>
    <div class="big"><img src="http://placehold.it/300x200" /></div>
    <div class="normal"><img src="http://placehold.it/150x100" /></div>
    <div class="big"><img src="http://placehold.it/300x200" /></div>
    <div class="big"><img src="http://placehold.it/300x200" /></div>
    <div class="normal"><img src="http://placehold.it/150x100" /></div>    
  </nav>
</body>
</html>
```
[SOURCE](https://www.youtube.com/watch?v=-Wlt8NRtOpo) FreeCodeCamp.
