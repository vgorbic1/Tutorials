## Web Storage
Web storage can store data locally within the user's browser. It is more secure and faster than cookies.
The data is only used when asked for. The storage limit is at least 5 MB. The info in the storage is never
shared with the server. Data is stored in name-value pairs.

#### Objects for web storage
```javascript
window.localStorage // stores data with no expiration date
code.sessionStorage // stores data for one session only. Data is lost when browser's tab is closed.