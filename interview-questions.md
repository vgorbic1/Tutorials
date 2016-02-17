## Job Interview Questions
- [**Java**](https://github.com/vgorbic1/Tutorials/blob/master/Java/interview-questions.md)
- [**JavaScript**](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/interview-questions.md)
- [**PHP**](https://github.com/vgorbic1/Tutorials/blob/master/PHP/interview-questions.md)
- [**SQL**](https://github.com/vgorbic1/Tutorials/blob/master/SQL/interview-questions.md)

#### General Questions
**What are the differences between GET and POST methods in form submitting?**

A GET mostly used to retrieve data, usually through a URL where all parameters are visible. A POST is used for writing data and transfers info within the body of request, instead of URL.

**How can we submit a form without a submit button?**

- Using JavaScript: onClick event on the page triggers a function submit() in the script.
- Using PHP: using a header() function with a parameter location:script.php

**How can we get second of the current time using date function?**
- In PHP: `echo(date('s'));`
- In JavaScript: `var date = new Date();  var secs = date.getSeconds();`


