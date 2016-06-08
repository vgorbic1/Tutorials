## Login and Registration Script with PDO and OOP

Create Database And Table:
```sql
CREATE DATABASE `dblogin` ;
CREATE TABLE `dblogin`.`users` (
   `user_id` INT( 11 ) NOT NULL AUTO_INCREMENT PRIMARY KEY ,
   `user_name` VARCHAR( 255 ) NOT NULL ,
   `user_email` VARCHAR( 60 ) NOT NULL ,
   `user_pass` VARCHAR( 255 ) NOT NULL ,
    UNIQUE (`user_name`),
    UNIQUE (`user_email`)
) ENGINE = MYISAM ;
```
Create dbconfig.php
```php
<?php
session_start();
$DB_host = "localhost";
$DB_user = "root";
$DB_pass = "";
$DB_name = "dblogin";
try {
     $DB_con = new PDO("mysql:host={$DB_host};dbname={$DB_name}",$DB_user,$DB_pass);
     $DB_con->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $e) {
     echo $e->getMessage();
}

include_once 'class.user.php';
$user = new USER($DB_con);
```
#### Password hashing:
**password_hash()** For hashing password we have to use password_hash() function, the first parameter is password and second 
parameter used to specify the algorithm to hash password.
```php
<?php
     $password = "123456";
     $hash = password_hash($passwod, PASSWORD_DEFAULT);
     $hashed_password = "$2y$10$BBCpJxgPa8K.iw9ZporxzuW2Lt478RPUV/JFvKRHKzJhIwGhd1tpa";
     /* "123456" will become "$2y$10$BBCpJxgPa8K.iw9ZporxzuW2Lt478RPUV/JFvKRHKzJhIwGhd1tpa" */ 
?>
```
**password_verify()** For checking passwords, we have to use password_verify function, which checks a password string with a 
hashed password, then returns a boolean.
```
<?php
     $password = "123456";
     $hashed_password = "$2y$10$BBCpJxgPa8K.iw9ZporxzuW2Lt478RPUV/JFvKRHKzJhIwGhd1tpa";
     password_verify($password, $hashed_password);
     /* if the password match it will return true. */ 
?>
```
Create class.user.php
```php
this file must be included at the end of 'dbconfig.php' file. and creating a new object of this class file in the 'dbconfig.php' 
file we can make use of database,  this is the main class file which contains register(),login(),is_loggedin(),redirect() functions 
to maintain users activity. register() function register a new user with strong password hashing function.
```
<?php
class USER {
    private $db;
    function __construct($DB_con) {
      $this->db = $DB_con;
    }
 
    public function register($fname,$lname,$uname,$umail,$upass) {
       try {
           $new_password = password_hash($upass, PASSWORD_DEFAULT);
           $stmt = $this->db->prepare("INSERT INTO users(user_name,user_email,user_pass) 
                                                       VALUES(:uname, :umail, :upass)");
           $stmt->bindparam(":uname", $uname);
           $stmt->bindparam(":umail", $umail);
           $stmt->bindparam(":upass", $new_password);            
           $stmt->execute(); 
           return $stmt; 
       } catch(PDOException $e) {
           echo $e->getMessage();
       }    
    }
 
    public function login($uname,$umail,$upass) {
       try {
          $stmt = $this->db->prepare("SELECT * FROM users WHERE user_name=:uname OR user_email=:umail LIMIT 1");
          $stmt->execute(array(':uname'=>$uname, ':umail'=>$umail));
          $userRow=$stmt->fetch(PDO::FETCH_ASSOC);
          if($stmt->rowCount() > 0) {
             if(password_verify($upass, $userRow['user_pass'])) {
                $_SESSION['user_session'] = $userRow['user_id'];
                return true;
             } else {
                return false;
             }
          }
       } catch(PDOException $e) {
           echo $e->getMessage();
       }
   }
 
   public function is_loggedin() {
      if(isset($_SESSION['user_session'])) {
         return true;
      }
   }
 
   public function redirect($url) {
       header("Location: $url");
   }
 
   public function logout() {
        session_destroy();
        unset($_SESSION['user_session']);
        return true;
   }
}
?>
```
Create index.php as a login page which will take username or email id and password to access users home page if the details are 
wrong it will show appropriate message.
```php
<?php
require_once 'dbconfig.php';
if($user->is_loggedin()!="") {
 $user->redirect('home.php');
}

if(isset($_POST['btn-login'])) {
 $uname = $_POST['txt_uname_email'];
 $umail = $_POST['txt_uname_email'];
 $upass = $_POST['txt_password'];
  
 if($user->login($uname,$umail,$upass)) {
  $user->redirect('home.php');
 } else {
  $error = "Wrong Details !";
 } 
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>Login Page</title>
</head>
<body>
<div class="container">
     <div class="form-container">
        <form method="post">
            <h2>Sign in.</h2><hr />
            <?php
            if(isset($error)){
                  ?>
                  <div class="alert alert-danger">
                      <i class="glyphicon glyphicon-warning-sign"></i> &nbsp; <?php echo $error; ?> !
                  </div>
                  <?php
            }
            ?>
            <div class="form-group">
             <input type="text" class="form-control" name="txt_uname_email" placeholder="Username or E mail ID" required />
            </div>
            <div class="form-group">
             <input type="password" class="form-control" name="txt_password" placeholder="Your Password" required />
            </div>
            <div class="clearfix"></div><hr />
            <div class="form-group">
             <button type="submit" name="btn-login" class="btn btn-block btn-primary">
                 <i class="glyphicon glyphicon-log-in"></i>&nbsp;SIGN IN
                </button>
            </div>
            <br />
            <label>Don't have account yet ! <a href="sign-up.php">Sign Up</a></label>
        </form>
       </div>
</div>
</body>
</html>
```
Create signup.php, a registration page for registering a new user containing a form with three input box username, 
email and password, validations are given in this page and if username or user email already registered then it will show message 
that name or email already exists. it will handle registration process along with proper validations.
```php
<?php
require_once 'dbconfig.php';
if($user->is_loggedin()!="") {
    $user->redirect('home.php');
}

if(isset($_POST['btn-signup'])) {
   $uname = trim($_POST['txt_uname']);
   $umail = trim($_POST['txt_umail']);
   $upass = trim($_POST['txt_upass']); 
 
   if($uname=="") {
      $error[] = "provide username !"; 
   } else if($umail=="") {
      $error[] = "provide email id !"; 
   } else if(!filter_var($umail, FILTER_VALIDATE_EMAIL)) {
      $error[] = 'Please enter a valid email address !';
   } else if($upass=="") {
      $error[] = "provide password !";
   } else if(strlen($upass) < 6){
      $error[] = "Password must be atleast 6 characters"; 
   } else {
      try {
         $stmt = $DB_con->prepare("SELECT user_name,user_email FROM users WHERE user_name=:uname OR user_email=:umail");
         $stmt->execute(array(':uname'=>$uname, ':umail'=>$umail));
         $row=$stmt->fetch(PDO::FETCH_ASSOC);
    
         if($row['user_name']==$uname) {
            $error[] = "sorry username already taken !";
         } else if($row['user_email']==$umail) {
            $error[] = "sorry email id already taken !";
         } else {
            if($user->register($fname,$lname,$uname,$umail,$upass)) {
                $user->redirect('sign-up.php?joined');
            }
         }
     } catch(PDOException $e) {
        echo $e->getMessage();
     }
  } 
}

?>
<!DOCTYPE html>
<html lang="eng">
<head>
<meta charset="utf-8" />
<title>Sign up Page</title>
</head>
<body>
<div class="container">
     <div class="form-container">
        <form method="post">
            <h2>Sign up.</h2><hr />
            <?php
            if(isset($error)) {
               foreach($error as $error) {
                  ?>
                  <div class="alert alert-danger">
                      <i class="glyphicon glyphicon-warning-sign"></i> &nbsp; <?php echo $error; ?>
                  </div>
                  <?php
               }
            } else if(isset($_GET['joined'])) {
                 ?>
                 <div class="alert alert-info">
                      <i class="glyphicon glyphicon-log-in"></i> &nbsp; Successfully registered <a href='index.php'>login</a> here
                 </div>
                 <?php
            }
            ?>
            <div class="form-group">
            <input type="text" class="form-control" name="txt_uname" placeholder="Enter Username" value="<?php if(isset($error)){echo $uname;}?>" />
            </div>
            <div class="form-group">
            <input type="text" class="form-control" name="txt_umail" placeholder="Enter E-Mail ID" value="<?php if(isset($error)){echo $umail;}?>" />
            </div>
            <div class="form-group">
             <input type="password" class="form-control" name="txt_upass" placeholder="Enter Password" />
            </div>
            <div class="clearfix"></div><hr />
            <div class="form-group">
             <button type="submit" class="btn btn-block btn-primary" name="btn-signup">
                 <i class="glyphicon glyphicon-open-file"></i>&nbsp;SIGN UP
                </button>
            </div>
            <br />
            <label>have an account ! <a href="index.php">Sign In</a></label>
        </form>
       </div>
</div>
</body>
</html>
```
