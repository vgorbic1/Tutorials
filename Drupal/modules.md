## Useful Modules

#### Context
Do you need to do something different with one part of your site? Context is ideal for dividing your site into sections, based on various criteria, and apply different "reactions" to those sections. You can create a section based on content type, menu path, taxonomy term, user roles, and more. Reactions include:
* add blocks to regions;
* control which menu item is active;
* add different titles and subtitles;
* add a unique class to the HTML body tag.

#### jCarousel
This module makes the popular jCarousel plug-in available to Drupal. jCarousel is normally used to display and scroll multiple images in a row. There are many configuration options, and it's simple to turn any view into a jCarousel.

jCarousel isn't just for images either. Pretty much anything Views can output can be put into a jCarousel. There are several simple themes included, or you can completely override the designs with your own images and CSS.

#### Views slideshow
This is another way of creating slideshows in various configurations. It is very similar to jCarousel, and has very similar usage and configuration options. Instead of displaying several images in a row, however, Views Slideshow is best used when displaying and scrolling one image at a time.

Wondering which carousel module to use? jCaoursel is great if you want to display and scroll multiple images in a row (or column). Views slideshow is better if you want to display one image at a time. Both modules allow you to include other content – pretty much anything you can add to a View, you can add to a slideshow.

#### Colorbox
There are many JavaScript Lightbox scripts out there. These modules allow you to link a photo (or text, or whatever), to a large version of the image, in a pop-up overlay. Colorbox is one of the few options with a well-maintained Drupal implementation. The module integrates well with both fields and Views. You can easily set an image field or View to display in a colorbox. It also provides a very powerful colorbox trigger field to Views, which can allow you to do some pretty neat things.

Lightbox2 and Shadowbox are two other useful options. I personally found Colorbox to have more usable controls within Drupal than Lightbox2, and Shadowbox requires a lisence for commercial use. The comparison of Lightbox-type modules is currently rather out of date but may be helpful.

#### Menu block
It's simple to display a flat list of menu links, but what if you want to something different? What if you want the whole tree? Or part of a tree? It's common for a design to show a top-level set of links in a horizontal menu, with related sub-navigation in a sidebar. How do you do that?

Enter Menu block. This module can output sections of a menu tree in different configurations. You can also configure menu blocks to follow the active page, which makes it possible to create one menu block for each sub-section of a menu. Make sense? I hope so. The configuration options can be rather confusing, but with a little fliddling you can get just about any menu output you could wish for.

#### Contact form blocks
The default Drupal contact form isn't exactly the most configurable thing in the world. Changing the title or adding intro text can be a pain. And what if you want to have multiple contact forms in different places on your site? Or maybe your designer has done something wacky like put the form in a footer or sidebar. 

The Contact form blocks module exposes contact forms as blocks. You could add one to a simple page containing the rest of your contact information, making the content easier for clients to edit themselves. Each contact form category gets its own block, so you can have different types of forms (going to different people), in different locations on the site. The settings for the module allow you to select which categories should have blocks available.

#### Conditional Stylesheets
You could create your own html.tpl.php and put CSS there. Or you could use the drupal_add_css() function in your template.php file. Or you could use a module created especially for this purpose.

Conditional Stylesheets allows you to add special stylesheet files for IE, based on the conditional comment syntax, in your theme's .info file. The module will then insert the stylesheets in the <head> of every page along with the rest of your CSS files.

#### Devel/Devel generate/Devel themer
Devel is a module created especially for developers, but it also has some add-ons that are very useful for thememers and site-builders like you.

Getting clients to deliver content ahead of time is wishful thinking. But we all need something to work with while developing content types and associated views, taxonomies, menus, and template files. This is where devel generate comes in. It can create node content, taxonomy terms, menus, users, and more. Just tell it what you want it to create, and off it goes!

Devel themer is an associated module that is created just for themers. This module provides lots of information that primarily helps you to figure out where a certain bit of code comes from. Is there a template file for that? A theme function? If your best guesses aren't getting you anywhere, devel themer will help you out.

Devel themer can mess up the display of your theme. It's best to turn it on when you need it and turn it off again when you're done.

#### Panels
Panels allows you to create customized layouts inside your existing page template. A panel layout is like a mini template with its own regions that sits inside your existing content area. You can also disable your existing regions, allowing Panels to take over the entire layout.

Panels has a visual user interface for placing content in panels, making it easy to place particular blocks in the correct place in the layout. You can choose from pre-defined layouts, or design your own. There is a drag-and-drop interface for creating the layout but it generates crufty HTML. Instead, it is a better idea to create your own layout. In Panels, custom layouts are contained in the theme folder, with their own template files and CSS.

Panels does quite a lot more. For example, you can also create "mini-panels", which act as blocks. It comes with alternate layouts for nodes, user profiles, and taxonomy pages. You can customize the display of blocks within your panel by adding additional rules (e.g. user has a certain role). Panels allows you to apply your own CSS classes to the panel layout and id's to individual panels. 

The stylesheet for your panels layout will be inserted before the rest of your theme CSS (standard for Drupal - module CSS comes first then theme CSS). This means that you might have to use more specificity than you otherwise would when you need to override your theme CSS. The stylesheet for your panels layout will also be used in the panels admin interface. This means that you might need to add in some extra selectors to keep this layout clean. You probably want to keep the base row/column layout here but not not apply too much additional styling.
