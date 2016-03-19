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
Create an empty text file called `page.tpl.php`. In here will go all the code for the main <body> section of your theme. This file consists of three elements: the HTML mark-up for your theme (containing div's, and any other major structural elements), region definitions, variables for other content items (e.g. title, navigation tabs). Start by creating the basic HTML structure for your page:
```html
<div id="header"></div>

<div id="wrapper">
  <div id="content"></div>
  <div id="sidebar"></div>
</div>

<div id="footer"></div>
```
Create regions. Any part of your page that you want to be editable in the Drupal interface (via Blocks) needs to become a region. In our sample site, this includes header, right sidebar,  content area, and footer. Don't forget that all of your regions need to be introduced in the `.info` file first. Drupal will provide a set of default regions if you don't specify any regions. Theoe include header, highlighted, help, content, sidebar_first and sidebar_second. 

In Drupal 7 variables, including regions, are inserted using **Render Arrays**. With the exception of the content region, there is a chance that the region will be empty (e.g. if there are no blocks placed in a given region). You probably don't want anything to be printed if the regions are empty. These variables need to be surrounded by conditionals, checking to make sure they exist. The following code creates a conditional to check that the footer region has something in it, then prints out the contents:
```PHP
<?php if ($page['footer']): ?>    
  <?php print render($page['footer']); ?>
<?php endif; ?>
```
Repeat this code for each of your regions, replacing the $page['footer'] variable with the machine names of your regions (the ones in the square brackets in your `.info file`). The content section is an exception, in that it does not need to be surrounded by a conditional statement beacuse there will always be something in the content region.

Sample page.tpl.php:
```PHP
<div id="header">
  <?php if ($page['header']): ?>    
    <?php print render($page['header']); ?>
  <?php endif; ?>
</div>

<div id="wrapper">
  <div id="content">
    <?php print render($page['content']); ?>
  </div>

  <?php if ($page['sidebar_first']): ?>    
    <div id="sidebar">
      <?php print render($page['sidebar_first']); ?>
    </div>
  <?php endif; ?>  
</div>

<div id="footer">
  <?php if ($page['footer']): ?>    
    <?php print render($page['footer']); ?>
  <?php endif; ?>  
</div>
```
There are other parts of the page that exist outside of regions. At this stage we will add variables for key page elements, including the page title and Drupal navigation tabs. There are many other variables available to `page.tpl.php`. What you include depends on what functionality you want your theme to have. Do you want breadcrumbs? If so, put in the `$breadcrumbs` variable.

Some of the most common are:
* `$site_name`
* `$logo` (the logo uploaded through the theme settings; only useful when you're implementing the logo theme feature)
* `$title` (the page title)
* `$main_menu`
* `$secondary_menu`
* `$breadcrumbs`

There are also some variables associated with Drupal administration:

* `$tabs` (menu used for edit/view admin menus, among other things; often used by modules)
* `$messages`
* `$action_links`

And some other useful  variables:

* `$base_path` (the path to your site root)
* `$front_page (the path to the site front page)
* `$directory` (the path to your theme)
Variables are inserted using the Render API, like this:
```PHP
<?php print render($tabs); ?>
```
In Drupal 7 there are now `$title_prefix` and `$title_suffix` variables. Modules may make use of these items, so it is important to include them in all themes.

Some variables need to be displayed using the `render()` function, while others can simply be printed. How do you know the difference? If there variable is an array (as listed on the `page.tpl.php` reference page), you need to use `render()`. If not, you can just print the variable `<?php print $variable; ?>`. If you're having trouble you can also check the default `page.tpl.php` and see how they did it there.

#### Menus and Theme Settings
Blocks for the standard navigation menus (main menu and secondary menu) are provided by default but they are also available as variables. You could use either method for inserting the links into your page template. If you want to be able to move them around easily, they should be blocks. Otherwise they can be hard-coded into the template using variables if you prefer.

Similar logic can be used for determining which way to display other common site elements such as the logo. Do you want to be able to easily change the logo through the admin interface or turn the main menu off? If so, use the theme settings and associated variable. If not the variable can be placed directly into the page template.

The desirability of being able to manipulate these elements within the admin interface depends on the purpose of your theme. If this is a generic theme, to be used by many different sites, it is probably a good idea to make it easy to change the placement of navigation menus, or to upload a new logo. If you are designing a site for a client, on the other hand, you might not want them to change the logo or move around the navigation menus.

Another important point is that menu links are returned as an array. When you include this in your page template, you need to expand it by sending it through theme() which will expand the array:
```PHP
<?php if ($main_menu): ?>
  <?php print theme('links__system_main_menu', array('links' => $main_menu, 'attributes' => array('id' => 'main-menu'))); ?>
<?php endif; ?>
```
Sample page.tpl.php file:
```PHP
<div id="wrapper">

  <div id="header">
    <a href="<?php print $front_page;?>">
      <img src="/<?php print $directory;?>/images/logo.png" alt="<?php print $site_name;?>" height="80" width="150" />
    </a>
 
    <?php if ($main_menu): ?>
      <?php print theme('links', $main_menu); ?>
    <?php endif; ?>

  </div>
 
  <div id="content">
    <?php print render($title_prefix); ?>
      <?php if ($title): ?><h1><?php print $title; ?></h1><?php endif; ?>
    <?php print render($title_suffix); ?>

    <?php print render($messages); ?>
    <?php if ($tabs): ?><div class="tabs"><?php print render($tabs); ?></div><?php endif; ?>
    <?php if ($action_links): ?><ul class="action-links"><?php print render($action_links); ?></ul><?php endif; ?>

    <?php print render($page['content']); ?>
  </div>

  <?php if ($page['sidebar_first']): ?>    
    <div id="sidebar">
      <?php print render($page['sidebar_first']); ?>
    </div>
  <?php endif; ?>  

  <div id="footer">
    <?php if ($page['footer']): ?>    
      <?php print render($page['footer']); ?>
    <?php endif; ?>  
  </div>

</div>
```

#### Build your CSS
This step works pretty much the same way as it would on any other site. If you make some changes and don't see them reflected on your site, try clearing the theme registry (cache) by going to Site Configuration > Performance and clicking the button to clear cached data. Click the little "+" button next to the title on the Performance page to add this to your custom toolbar.

#### Create your screenshot
In the Drupal admin interface a screenshot will appear next to your theme name. To make this image, simply create a screenshot of your finished site, resize and crop to 150x90, and place it in your theme directory. It should be named screenshot.png. Drupal does have some guidelines on creating a screenshot file, but these only need to be followed if you intend to contribute your theme to the Drupal theme repository.

[SOURCE](http://www.apaddedcell.com/how-create-drupal-7-theme-scratch)
