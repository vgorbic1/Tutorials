## Displaying random image
```php
<?php
$images = array('myimage', 'another_image');
$index =  rand(0, count($images)-1);
$selectImage = "images/{$images[$index]}.jpg";
?>
```
and on the page
```html
<img src="<?php echo $selectImage; ?>"
```
To allow for captures, instead of on one array create another associative array that will represent each image and iclude those arrays into the original array.
