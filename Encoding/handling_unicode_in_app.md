## Handling Unicode Front To Back In A Web App
This article shows how to get a PHP web application with a MySQL database set up to handle UTF-8 data front to back. We'll assume an application that needs to accept input of and output text containing any imaginable character currently supported by computers. For testing purposes, we'll use this block of text:
```
A good day, World!
Schönen Tag, Welt!
Une bonne journée, tout le monde!
يوم جيد، العالم
좋은 일, 세계!
Một ngày tốt lành, thế giới!
こんにちは、世界！
```
If the text ever appears any different at any stage in your app, you have an encoding problem somewhere. The goal is to hardcode this text in an HTML/PHP file and have it display correctly in the browser. Further, we want to allow a user to input this text in a form, save it in a MySQL database, retrieve it again from the database and display it back on the page. The text should be stored correctly in the database, so when looking at the database content in a database admin utility or when searching for content, it will be displayed and found correctly.

Handling encodings correctly within one system is not hard. Problems usually arise when exchanging data between two different systems. In our application, there will be two such interfaces between systems:
- PHP to browser/browser to PHP
- PHP to MySQL/MySQL to PHP
Text is exchanged as binary data behind the scenes. This series of bits and bytes may represent anything at all; what exactly it represents depends on the encoding it was created with and which it is interpreted with. Since the text itself does not specify what it was encoded with, this information needs to be transported as meta information between different systems.

