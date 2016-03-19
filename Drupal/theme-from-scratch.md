## Create a Theme from Scratch (Drupal 7)
Working from scratch will help you to gain a better understanding of the theming system.

#### Create the Folder Structure
First you need to create a folder for your new theme. This should go in `sites/all/themes` or `sites/yoursite/themes` depending on whether this theme should be available to all sites on your installation or just one site. Give the folder a unique name that describes your theme (no spaces). Include sub-folders for images and CSS files.

#### Create the .info File
This is a simple text file with a .info extension. The name you give this file will be used by Drupal internally. Inside the .info file, we’ll need to enter information about our theme in key-value pairs:
* `name` - a human-readable name of your theme.
* `description` - a description of the theme.
* `core` - the version of Drupal this is designed for.
* `engine` - the templating engine your theme will use (probably phptemplate)
* `regions` - the block regions available. The machine name of the region is included in square brackets (e.g. `regions[sidebar_first]`). This will be used to insert the region into your template files. The label you assign to it will be used in the admin interface when assigning blocks to your regions. In Drupal 7 you must include the content region in addition to any custom regions you need for your theme. It is a good idea to use the standard Drupal names for sidebar regions ("sidebar_first" and "sidebar_second" in Drupal 7). This will enable Drupal to add classes to the <body> tag to indicate which sidebars are in use (no-sidebars, sidebar-right, sidebar-left).
* `features` - theme components that can be turned on or off in in the Drupal admin interface (e.g. option to specify a site name, mission statement, logo etc.). Only the features listed in your .info file will be available on the admin page and as variables in your page template. If you want to clear all features, leave it blank. To include all features, omit the features item entirely.

*Using custom theme settings (features)* Some of these elements specified in the `features` key may not be necessary for your theme. By default, blocks are available for the standard navigation menus (main menu and secondary menu). The theme will pick up the shortcut icon (favicon.ico) file in your theme directory. You may prefer to code your logo image in your page template rather than uploading one through the admin interface. Specifying these options is only necessary if you want to code the variables into your template file and/or allow users to turn them on or off in the theme admin settings.
* `stylesheets` - your CSS files. The media type is included in the first set of square brackets (e.g. `stylesheets[all][]` or `stylesheets[print][]`)
* `scripts` - any scripts required by your template (remember that Drupal comes with jQuery, so you don't need to include it here). The scripts and stylesheet values are relative to the theme directory (i.e. the `/sites/yoursite/themes/yourtheme` path is automatically included). If you want to specify a file outside this directory you need to enter the path relative to the theme directory.

Here is a sample .info file:
```
name = My Cool Theme
description = Custom theme for my site
core = 7.x
engine = phptemplate

regions[header] = Header
regions[sidebar_first] = Right sidebar
regions[content] = Content
regions[footer] = Footer

stylesheets[all][] = css/style.css
stylesheets[print][] = css/print.css

features[] = name
features[] = main_menu
```

#### Drupal Template Files
Drupal themes are based on template files, defined with the extension `.tpl.php`. These files contain the html for your theme, as well as some variables that tell Drupal where to put things.

If you want to create a very simple theme, you actually don't need to have any template files at all. Your theme could be just CSS. Drupal comes with default template files for all of the code it outputs. These defaults are included with the module that generates the content for a particular element. For example, the html mark-up for a node is included with the node module as `node.tpl.php`. The html code for a block is included with the block module in the `block.tpl.php` file.

You only need to create your own version of a template file if there is something you want to change from the defaults. Otherwise, Drupal will simply use the default file. It is never a good idea to make changes to the default ("core") files in Drupal. Always use the proper method for overriding code in your theme. 

To create your own version of a template file, copy the default version from the module folder that created it, and place it in your theme folder. Sometimes it could be difficult to determine which module created a particular piece of code.

In Drupal 7 there is also an html.tpl.php template, which includes code for the overall structure of the document (the doctype, the <head> section, and opening and closing <body> and <html> tags). 

The most important template file, and the one you will most likely want to change, is the `page.tpl.php`. This template file contains the code for the body of the page. The default `page.tpl.php` file is contained in the system module. The default does contain a lot of extra options that you might not need, so let's write our own page.tpl.php from scratch.

#### Create the page.tpl.php File
