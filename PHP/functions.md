## Functions

#### Handling variable-length argument lists. (Similar to overloading in Java)
PHP provides three built-in functions to handle variable-length argument lists:
- func_num_args()
- func_get_arg()
- func_get_args()

```php
function hello() {
  if (Func_num_args() > 0) {
    $arg = func_get_arg(0);
    echo "Hello $arg";
  } else {
    echo "Hello World";
  }
}

hello("Reader"); // displays "Hello Reader"
hello(); // displays "Hello World"
```

