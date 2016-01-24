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

#### Browser
To specify to the browser what kind of content you are giving it, there's the HTTP Content-Type header:
```
Content-Type: text/html; charset=utf-8
```
There are also the HTML meta tags:
```
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
```
and its newer HTML5 version
```
<meta charset="utf-8" />
```
These tags are only fallbacks though which are only used when no HTTP Content-Type header was encountered (the wording "http-equiv" hints at this). So, the web server should always emit an HTTP header specifying the site's type and encoding. This can be configured in the web server itself, or it can be done using PHP by using header somewhere at the start of the application, before any content has been output:
```PHP
header('Content-Type: text/html; charset=utf-8');
```

#### Form
So the browser knows how to interpret data that your web server sends to it. How should the web server know how to interpret data sent to it by the browser? The default behavior is that the browser will reply to the server in the same encoding that the server sent content to it. So by setting the above Content-Type header, you're pretty much already set to receive UTF-8 encoded data from the browser. To make this really explicit, you can set the accept-charset attribute on forms:
```
<form action="action.php" accept-charset="utf-8">
```

#### Database
When connecting to the database, there's an implicit or explicit connection encoding. That means any textual data you send over this connection, the database will interpret in that encoding and any textual data you receive from the database will be encoded in that encoding. 
```sql
CREATE TABLE `texts` (
  `id` INT(11) unsigned NOT NULL AUTO_INCREMENT,
  `content` TEXT,
  PRIMARY KEY (`id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```
This creates a table with a default character set of UTF-8. This does not actually mean anything yet, since the encoding is specific per text column. Any column that does not explicitly specify an encoding will be set to this DEFAULT CHARSET. Consider this:
```sql
CREATE TABLE 'texts' (
  'id' INT(11) unsigned NOT NULL AUTO_INCREMENT,
  'text' TEXT CHARACTER SET latin1,
  PRIMARY KEY ('id')
) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```
