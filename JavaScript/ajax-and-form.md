## Ajaxifying Existing Form
You can use jQuery `$.serialize()` to easily ajaxify existing POST forms without fiddling around with collecting and passing the individual form input parameters. Assuming an existing form which works perfectly fine without JavaScript/jQuery:
```html
<form id="someform" action="someservlet" method="post">
    <input type="text" name="foo" />
    <input type="text" name="bar" />
    <input type="text" name="baz" />
    <input type="submit" name="submit" value="Submit" />
</form>
```
You can ajaxify it:
```javascript
$(document).on("submit", "#someform", function(event) {
    var $form = $(this);
    $.post($form.attr("action"), $form.serialize(), function(responseJson) {
        // ...
    });
    event.preventDefault(); // Important! Prevents submitting the form.
});
```
You can in the servlet distinguish between normal requests and ajax requests as below:
```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String foo = request.getParameter("foo");
    String bar = request.getParameter("bar");
    String baz = request.getParameter("baz");

    boolean ajax = "XMLHttpRequest".equals(request.getHeader("X-Requested-With"));

    // ...

    if (ajax) {
        // Handle ajax (JSON) response.
    } else {
        // Handle regular (JSP) response.
    }
}
```
The jQuery Form plugin does less or more the same as above jQuery example, but it has additional transparent support for `multipart/form-data` forms as required by file uploads.
