## How to

### Create a script based local scope?
```js
function main() {
  // this variables will be in local scope for the main() function
  // preventing global scope polution
  const a = document.querySelector(".someClass");
  const b = 'hello';
  const c = function () {
    a.innerText = b;
  }
  
  c();
}

window.onload = main;
```
