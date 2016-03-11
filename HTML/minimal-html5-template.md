## A Minimal HTML5 Document
Because all browsers (even old ones like IE6) fully support the standardized HTML5 shortcuts, we can use:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>title</title>
    <link rel="stylesheet" href="style.css">
    <script src="script.js"></script>
  </head>
  <body>
    <!-- page content -->
  </body>
</html>
```
* Every HTML document should start with a `<!DOCTYPE>` declaration that tells the browser what version of HTML the document is written in. This code has been specifically designed to “fool” current browsers (that are yet to support HTML5) into treating the document as a full-blooded HTML4 document. Browser versions as far back as Internet Explorer 6 will render the page with their most standards-compliant rendering mode.
* The `<html>` tag should should specify the primary language for the document’s content with the a attribute.
* The first bit in the header should be a <meta> tag that specifies the character encoding of the page. Usually, the character encoding is declared by the web server that sends the page to the browser, but many servers are not configured to send this information. Specifying it here ensures the document is displayed correctly even when it’s loaded directly from disk, without consulting a server.
* In CSS declaration, the `type="text/css"` and `type="text/javascript"` attributes that was required in HTML4 are now optional in HTML5, and all current browsers know what to do if you leave those attributes out.
