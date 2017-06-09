## Meta Boxes
WordPress features multiple sections, or meta boxes, on the post, page, and link manager screens.
These meta boxes enable you to easily add additional data to your content.

To create a custom meta box in WordPress, you use the `add_meta_box()` function. This function
enables you to define all aspects of your meta box. Following is how this function is used:
```php
<?php add_meta_box( id, title, callback, page, context, priority, callback_args ); ?>
```
The `add_meta_box()` function accepts the following parameters:
- id — The CSS ID added to the DIV element that wraps your meta box
- title — The name of your meta box displayed in its heading
- callback — Function to be called to display your meta box
- page — The screen where your meta box should show
- context — The part of the page where the meta box should be shown
- priority — The priority in which your meta box should be shown
- callback_args — Arguments to pass into your callback function


