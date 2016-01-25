## Form validation
Always validate data in HTTML forms before sending it to a server.
- All required fields covered?
- Validate e-mail address.
- Valid data?
- No text in numeric fields?

#### Required fields
To check whether required field is filled in, use this script:
```javascript
function validateForm() {
  x = document.forms['myForm']['file'].value;
  if (x == null || x == "") {
      alert("no data in dields");
      return false;
  }
}
```
