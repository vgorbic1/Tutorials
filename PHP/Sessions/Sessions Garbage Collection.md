## Session Garbage Collection
Session is usually used by websites to keep track of various user related information across some period of time. 
PHP provides session garbage collection mechanism that ensures old unused sessions to be cleared regularly. This 
will help to prevent performance degrade due to filling up of session data and to reduce the risk of session 
hijacking as well.

The parameters that control this garbage collection process are *session.gc_maxlifetime*, *session.gc_probability*,
and *session.gc_divisor* in the PHP configuration file php.ini. 
- *session.gc_maxlifetime* defines the number of seconds 
to be elapsed before session data is seen as garbage and cleaned up by the garbage collection process. It represents 
the minimum amount of time that garbage collection allows an inactive session to exist. 
- *session.gc_probability* and session.gc_divisor define the probability that the garbage collection process is run 
on every session initialization. For example, if session.gc_probablility is set to 1 and session.gc_divisor is set 
to 100, then the probability of 0.01 (= session.gc_probability / session.gc_divisor) indicates that there is a 
1% chance that the garbage collection process runs on each session initialization request. Setting the probability 
too high will add unnecessary processing load on the server whereas setting it too low may cause server performance 
to degrade due to large amount of stored session data (whether needed or not) and increase the risk of user 
reconnecting to an old unwanted session as well (whether maliciously or not).

Use this code before *session_start()* to run garbage collection in 60 seconds:
```php
ini_set('session.gc_maxlifetime', 60);
session_set_cookie_params(60);
```
