## Onload function of XMLHttpReaquest
There is a new function added to XMLHttpRequest object:
```javascript
// The older way:
document.getElementById('button').addEventListener('click', loadData);

function loadData() {
  // Create an XHR Object
  const xhr = new XMLHttpRequest();
  
  // Fetch data 
  xhr.onreadystatechange = function() {
     console.log('READYSTATE', xhr.readyState);
     if(this.status === 200 && this.readyState === 4){
       console.log(this.responseText); // responseText is data from the file
     }
  }
  
  // Get data from file
  xhr.open('GET', 'data.txt', true);
  xhr.send();
}
```
```javascript
// Modern way:
document.getElementById('button').addEventListener('click', loadData);

function loadData() {
  // Create an XHR Object
  const xhr = new XMLHttpRequest();
  
  // Optional - used for spinners/loaders
  xhr.onprogress = function(){
    ... // do something
  }
  
  // Fetch data 
  xhr.onload = function() {
    console.log('READYSTATE', xhr.readyState);
    if(this.status === 200) {
      // console.log(this.responseText);
    }
  }
  
  // Get data from file
  xhr.open('GET', 'data.txt', true);
  
  // If Error happens (good practices to include)
  xhr.onerror = function() {
    console.log('Request error...');
  }
  
  xhr.send();
}
```
