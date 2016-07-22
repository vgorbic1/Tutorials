## Loops

#### foreach
This loop is designed for cycling through values stored in an array. 

Syntax:
```
foreach ($customers as $customer) {    where $customers is an array we are looping through
    echo $customer;                    and $customer is just a temporary variable
}
```
Example:
```php
foreach ($_POST['todelete'] as $delete_id) {
    // Delete a row from the table
};
```
The array ‘todelete’ may be formed by cycling through all checkboxes in the table:
```php
while ($row=mysqli_fetch_array($result)) {
  echo '<input type="checkbox" value="' .
       $row['id'] . '" name="todelete[]">';
};
```
