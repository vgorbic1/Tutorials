## Cookies
Cookies mostly used to keep you logged in so that you can keep going back without having continually reenter the username and password. Cookies are set and retrieved by web browser via headers.
To set cookie:
setcookie(‘username’, ‘FJones’, time() + 60 * 60 * 24 * 7);
To read cookie:
$username = isset($_COOKIE[‘username’]) ? $_COOKIE[‘username’] : FALSE;
You can read cookie only after they are set. Probably on the consecutive page load.
To delete cookie:
setcookie(‘username’, ‘’, time() – 3600);

Browser Identification
To extract browser info from the user agent string use GetBrowser() function:
<!DOCTYPE html>
<html>
  <head>
    <title>Browser Detecting</title>
  </head>
  <body>
<?php
  echo '<b>Your browser is</b>: '        . GetBrowser() . '<br>';
  echo '<b>Your user agent string</b>: ' . $_SERVER['HTTP_USER_AGENT'];

  function GetBrowser()
  {
    $UA = $_SERVER['HTTP_USER_AGENT'];

    if     (strstr($UA, 'MSIE'))    return 'IE';
    elseif (strstr($UA, 'Trident')) return 'IE';
    elseif (strstr($UA, 'Opera'))   return 'Opera';
    elseif (strstr($UA, 'OPR'))     return 'Opera';
    elseif (strstr($UA, 'Chrome'))  return 'Chrome';
    elseif (strstr($UA, 'iPod'))    return 'iPod';
    elseif (strstr($UA, 'iPhone'))  return 'iPhone';
    elseif (strstr($UA, 'iPad'))    return 'iPad';
    elseif (strstr($UA, 'Android')) return 'Android';
    elseif (strstr($UA, 'Safari'))  return 'Safari';
    elseif (strstr($UA, 'Firefox')) return 'Firefox';
    elseif (strstr($UA, 'Gecko'))   return 'Firefox';
    else                            return 'Unknown';
  }
?>
  </body>
</html>
