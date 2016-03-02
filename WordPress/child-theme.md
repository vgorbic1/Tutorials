## How to Create a Child Theme

Child themes allow you to make changes without affecting the original theme’s code, which makes it easy to update your parent theme without erasing your changes. Not only does this make updating easier, it also makes sure that you will never ruin your original theme as you are never actually modifying the files.

#### Getting Started
First things first, we need to create a new folder for your child theme. Naming it something like /foxy-child/ is conventional. Within your new theme folder, create a file called style.css and fill in the information as outlined below. The theme Name, URI, Description and Author are totally up to you:
```css
/*
 Theme Name:     Foxy Child Theme
 Theme URI:      http://www.elegantthemes.com/gallery/foxy/
 Description:    Foxy Child Theme
 Author:         Elegant Themes
 Author URI:     http://www.elegantthemes.com
 Template:       Foxy
 Version:        1.0.0
*/
 
@import url("../Foxy/style.css");
 
/* =Theme customization starts here
------------------------------------------------------- */
```
“Template:” parameter should correctly identifies the name of your parent theme. @import sections identifies the parent theme imports the CSS from the original. You must ensure that the path to your parent theme’s css file is correct. Everything must be case sensitive! The folder of our parent theme is “Foxy” with a capital F, and the @import URL reflects this.

#### Activating Your Child Theme
upload and activate your new child theme. Uploading and activating a child theme is no different than a normal theme, simply upload it via the Appearances > Themes page in your WordPress Dashboard and activate it.

#### Modifying Your Theme’s CSS
To modify your theme’s CSS, you can add any changes to your child theme’s CSS file below the @import line. All new CSS information is added after the original theme’s CSS is loaded. Because our new CSS is located below the original’s in the file, all new CSS styles will overwrite the original’s.

#### Editing The Functions File
Functions.php is where a theme’s main functions are typically stored. A parent theme’s functions are always loaded with the child theme, but if you need to add more custom functions to your theme then you can do so by creating a new functions.php file within your child theme folder. The new functions will be loaded right before the parent theme’s functions. 

#### Editing Other Template Files
Unlike editing the functions.php, where the original theme’s functions are imported automatically, PHP files are edited by replacing the file entirely with a new one. The theme’s original file is ignored and the new one is used instead. The first thing we need to do is replicate the old file before we start to modify it.
