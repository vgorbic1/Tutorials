##Self-referencing Form

To make the self-referenceing more secure:
```php
<form action="<?php echo htmlspecialchars($_SERVER['PHP_SELF'], ENT_QUOTES, 'utf-8'); ?>"
      method="post">
```
