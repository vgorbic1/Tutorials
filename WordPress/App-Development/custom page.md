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

The shortcode technique
should not be used in web applications due to the lack of control it displays within
the source code. Even though page templates are not the best solution, we can use
them for advanced requirements in web applications.

WordPress uses a function called `get_template_part` for reusing templates as
pure PHP files. This function locates the given template parts inside your theme
files and makes a file inclusion under the hood.
```php
get_template_part( $slug, $name );
```
The first parameter, $slug, is mandatory, and it is used to load the main template.
The second parameter, $name, is optional, and it is used to load a specialized
version of the template.
```php
get_template_part("project");
get_template_part("project", "wordpress");
```
The first line of code will include the project.php file inside the themes folder.
The second line of code will include the project-wordpress.php file, which will
be a specialized version of the project.php file in typical scenarios.

If you decide to use the WordPress technique of using template
files, make sure you create each and every template file inside
your theme folder.


