## Form Validation
The two primary approaches to validating an input are whitelisting and blacklisting. Blacklisting involves checking if the input contains unacceptable data while whitelisting checks if the input contains acceptable data. Since whitelisting tends to be both safer and more robust, it should be preferred for any validation routine. 

Input validation is frequently accompanied by a related process we call Filtering. Where validation just checks if data is valid (giving either a positive or negative result), Filtering changes the data being validated to meet the validation rules being applied. Where you must filter, always filter before validation and never after.

HTML forms are able to impose constraints on the input used to complete the form. You can restrict choices using a option list, restrict a value using a mininum and maximum allowed number, and set a maximum length for text. HTML5 is even more expressive. 
```
<form method="post" name="signup">
    <input name="fname" placeholder="First Name" required />
    <input name="lname" placeholder="Last Name" required />
    <input type="email" name="email" placeholder="someone@example.com" required />
    <input type="url" name="website" required />
    <input name="birthday" type="date" pattern="^d{1,2}/d{1,2}/d{2}$" />
    <select name="country" required>
        <option>Rep. Of Ireland</option>
        <option>United Kingdom</option>
    </select>
    <input type="number" size="3" name="countpets" min="0" max="100" value="1" required />
    <textarea name="foundus" maxlength="140"></textarea>
    <input type="submit" name="submit" value="Submit" />
</form>
```
However, any attacker can create a custom form that doesn’t include any of the constraints in your original form markup. For example, if a HTML form imposes a maxlength attribute but we receive input that exceeds that lenght, it may be wise to consider this as an attempted bypass of validation controls by a user. 

PHP is not a strongly typed language and most of its functions and operations are therefore not type safe. This can pose serious problems from a security perspective. Validators are particularly vulnerable to this problem when comparing values. When designing validators, be sure to prefer strict comparisons and use manual type conversion where input or output values might be strings. Web forms, as an example, always return string data so to work with a resulting expected integer from a form you would have to verify its type:
```PHP
function checkIntegerRange($int, $min, $max)
{
    if (is_string($int) && !ctype_digit($int)) {
        return false; // contains non digit characters
    }
    if (!is_int((int) $int)) {
        return false; // other non-integer value or exceeds PHP_MAX_INT
    }
    return ($int >= $min && $int <= $max);
}
```
You should never do this:
```PHP
function checkIntegerRangeTheWrongWay($int, $min, $max)
{
    return ($int >= $min && $int <= $max);
}
```


[Padraic Brady](http://phpsecurity.readthedocs.org/en/latest/Input-Validation.html)
