## Self-calling Form

#### Form
Use this form to update database:
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  <title>Add New User</title>
  <link rel="stylesheet" href="pure-min.css">
  <link rel="stylesheet" href="style.css">
  <script type="text/javascript" src="script.js"></script>
</head>
<body>

<?php
    require_once('connectvars.php');

    if (isset($_POST['submit'])) 
    {
        $dbc = mysqli_connect(DB_HOST, DB_USER, DB_PASSWORD, DB_NAME);

        $firstname = mysqli_real_escape_string($dbc, trim($_POST['firstname']));
        $lastname = mysqli_real_escape_string($dbc, trim($_POST['lastname']));
        $login = mysqli_real_escape_string($dbc, trim($_POST['login']));
        $password = mysqli_real_escape_string($dbc, trim($_POST['password']));

        // Lets check one more time in case JavaScript is turned off.
        if (!empty($firstname) && !empty($lastname) && !empty($login) && !empty($password)) {
            
            // Check if login exists
            $sql = mysqli_query($dbc, "SELECT login FROM users Where login='$login'");
            $result = mysqli_fetch_row($sql);
            if ( sizeof($result) > 0) {
                echo '<p class="error">Login already exists</p>';
                $form = true;
                
            } else {
        
                $query = "INSERT INTO users (first_name, last_name, login, password) VALUES ('$firstname', '$lastname', '$login', '$password')";
                mysqli_query($dbc, $query);
                mysqli_close($dbc);
            
                echo '<p class="success">The form is sucessfully submitted</p>';
                $form = false;
?>
<navigation>
  <div class="pure-menu pure-menu-horizontal">
    <ul class="pure-menu-list">
        <li class="pure-menu-item"><a class="pure-menu-link" href="manageusers.php">Manage Users</a></li>
        <li class="pure-menu-item"><a class="pure-menu-link" href="adduser.php">Add New User</a></li>
    </ul>
  </div>
</navigation>
<?php
            }
            
        }
        
        else {
            echo '<p class="error">All fields are required</p>';
            $form = true;
        }
    
    } else {
        $form = true;
    }
    
    if ($form) {

?>

  <form class="pure-form" enctype="multipart/form-data" method="post" action="<?php echo $_SERVER['PHP_SELF']; ?>" name="form">
    <label for="firstname">First Name:</label>
    <input type="text" id="firstname" name="firstname" value="<?php if (!empty($firstname)) echo $firstname; ?>" /><br />
    <label for="lastname">Last Name:</label>
    <input type="text" id="lastname" name="lastname" value="<?php if (!empty($lastname)) echo $lastname; ?>" /><br />
    <label for="login">Login:</label>
    <input type="text" id="login" name="login" value="<?php if (!empty($login)) echo $login; ?>" /><br />
    <label for="login">Password:</label>
    <input type="password" id="password" name="password" /><br /><br />
    <input type="submit" class="pure-button pure-button-active" value="Submit" name="submit" onclick="return validate();" />
  </form>
  <?php } ?>
</body> 
</html>
```
