## Fetch API
`fetch()` allows you to make network requests similar to XMLHttpRequest (XHR). 
The main difference is that the Fetch API uses Promises, which enables a simpler and cleaner API, avoiding 
callback hell and having to remember the complex API of XMLHttpRequest.

### Basic Fetch Request
Request a URL, get a response and parse it as JSON:
```js
fetch('./api/some.json')
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' +
          response.status);
        return;
      }

      // Examine the text in the response
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error :-S', err);
  });
```
### Response Type
To define the mode, add an options object as the second parameter in the fetch request and define the mode in that object:
```js
fetch('http://some-site.com/cors-enabled/some.json', {mode: 'cors'})
  .then(function(response) {
    return response.text();
  })
  .then(function(text) {
    console.log('Request successful', text);
  })
  .catch(function(error) {
    log('Request failed', error)
  });
```
### POST Request
It's not uncommon for web apps to want to call an API with a POST method and supply 
some parameters in the body of the request:
```js
fetch(url, {
    method: 'post',
    headers: {
      "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"
    },
    body: 'foo=bar&lorem=ipsum'
  })
  .then(json)
  .then(function (data) {
    console.log('Request succeeded with JSON response', data);
  })
  .catch(function (error) {
    console.log('Request failed', error);
  });
```
Form Data example:
```js
const formData = new FormData();
formData.append('name', name);
  fetch('template.php', {
      method: 'post',
      body: formData
    })
    .then(function(res) {
      return res.json();
    })
    .then(function(message) {
      console.log(message);
    })
    .catch(function(err) {
      console.log(err);
    });
```
