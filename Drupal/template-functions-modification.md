## Template and Functions Modification 

#### Template Customization Only in Particular Cases
Things get a bit complicated if you want to customize a template only in certain instances. You can customize templates for specific cases such as:
* The node template for a node type or a specific nod.
* The block template for a region or a specific block.
* The field template for a content type or a specific field.
* The taxonomy/term template for a vocabulary or a specific term.
* The comment template for a node type.
In these cases you need to rename the template file to tell Drupal when to use it. The general filename pattern is:
```
template--case.tpl.php
```
Note the two dashes between the name of the core template name and your use case. For example, if you want to customize the node template for a particular content type, you use the name of the content type as the case. To create a node template suggestion for the article content type only, you would rename your file to:
```
node--article.tpl.php
```
The machine name of the content type shown on the Content Types admin screen.

Drupal will use the most specific template available for a particular element. So, for example, if you provide a template suggestion for an individual node as well as for all nodes of that type, Drupal will use the one suggested for that particular node (because it's more specific). In some cases, a suggestion will only work if you've provided an instance of the base template (e.g. the above node template suggestion won't work unless you also have a `node.tpl.php` file in your theme).

Avoid adding PHP logic to your template files. These files are for structural mark-up only – logic goes elsewhere.

#### Overriding theme functions
Theme function overrides go into a file named `template.php`. This file should go in the root of your theme folder. First, create an empty file called `template.php`. When you've located the function you need to override, copy it to your `template.php` file and replace the `theme_` prefix with the machine name of your theme (the name you gave to your `.info` file). For example, to customize `theme_breadcrumb()`, you would change the name of the function to `yourtheme_breadcrumb()`.

[SOURCE](http://www.apaddedcell.com/change-html-output-drupal-7)
