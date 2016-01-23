# PHP
## Form Validation
The two primary approaches to validating an input are whitelisting and blacklisting. Blacklisting involves checking if the input contains unacceptable data while whitelisting checks if the input contains acceptable data. Since whitelisting tends to be both safer and more robust, it should be preferred for any validation routine. 

Input validation is frequently accompanied by a related process we call Filtering. Where validation just checks if data is valid (giving either a positive or negative result), Filtering changes the data being validated to meet the validation rules being applied. Where you must filter, always filter before validation and never after.


[Padraic Brady](http://phpsecurity.readthedocs.org/en/latest/Input-Validation.html)
