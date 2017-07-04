## Custom Pages for Web Applications

WordPress looks for a page with the slug
or ID before executing the default page.php file. In most scenarios, web application
layouts will take the other route of custom page templates, where we create a unique
template file inside the theme for each of the layouts and define it as a page template
using code comments.
```php
/*
* Template Name: My Custom Template
*/
```

Web application layout creation techniques:
- Static pages with shortcodes
- Page templates
- Custom templates with custom routing

