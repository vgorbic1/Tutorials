## Adding an image to a child theme
Using a parent theme (no child theme):
```
<img src="<?php echo get_template_directory_uri(); ?>/images/image.jpg" />
```
The basic difference, when using a child theme, is this:
- Template refers to the parent theme
- Stylesheet refers to the child theme
```
<img src="<?php echo get_stylesheet_directory_uri(); ?>/images/image.jpg" />
```
