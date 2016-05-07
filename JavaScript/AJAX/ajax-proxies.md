## Proxy
Proxy - a middleman between your local JavaScript file and remote server file.
#### Simple proxy application
```html
<html>
	<head>
		<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.2/jquery.min.js"></script>
		<script src="proxy.js"></script>
	</head>
	<body>
	</body>
</html>
```
JAVASCRIPT CLIENT
```javascript
$(document).ready(function() {
    $.get("proxy.aspx", function (data) {
        $(data).each(function (index, item) {
            alert(item);
        });
    }, "json");
});
```
PROXY (C# code)
```
// Create a request for the URL. 
WebRequest request = WebRequest.Create(
  "http://matcservice.azurewebsites.net/api/matc/");
WebResponse response = request.GetResponse();
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
Response.Write(responseFromServer);
reader.Close();
response.Close();
```
SERVICE (ASP.NET MVC Web API)
```
    public class MATCController : ApiController
    {
        // GET api/values
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5
        public void Delete(int id)
        {
        }
    }
  ```
