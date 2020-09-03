Headers 

# This is an h1 tag 
# hello 
## This is an h2 tag 
###### This is an h6 

# Emphasis

Emphasis, aka italics, with *asterisks* or _underscores_.

Strong emphasis, aka bold, with **asterisks** or __underscores__.

Combined emphasis with **asterisks and _underscores_**.

Strikethrough uses two tildes. ~~Scratch this.~~




# PHP 
Post Hypertext Protocol (made up)
No one really knows how it started

- PHP files can contain text, HTML, CSS, JavaScript, and PHP code
- PHP code is executed on the server, and the result is returned to the browser as plain HTML
- PHP files have extension ".php"

## Installing PHP
(Follow the LAMP stack guide)

## Basic PHP syntax 
PHP scripts can be placed anywhere in an exisiting HTML documnet, or can be placed in their own file.

An example of a very basic PHP file, within a html document:
```html
<!DOCTYPE html>
<html>
   <body>

      <h1>My first PHP page</h1>

      <?php
      echo "Hello World!";
      ?>

   </body>
</html> 
```

php has no keyword case sensitivity, this means that:
```
<?php
   ECHO "Hello World!<br>";
   echo "Hello World!<br>";
   EcHo "Hello World!<br>";
?>
```
is legal
However, all variable names are case sensitvie 
 
## Variables in PHP
Variables in php start with the `$` sign
```php
$txt = "george";
echo "Hello " + $txt;
```
Adding numbers:
```php
$x = 1;
$y = 2;
echo $x + $y;
```

php has 8 data types 

**Integers** − are whole numbers, without a decimal point, like 4195.

**Doubles** − are floating-point numbers, like 3.14159 or 49.1.

**Booleans** − have only two possible values either true or false.

**NULL** − is a special type that only has one value: NULL.

**Strings** − are sequences of characters, like 'PHP supports string operations.'

**Arrays** − are named and indexed collections of other values.

**Objects** − are instances of programmer-defined classes, which can package up both other kinds of values and functions that are specific to the class.

**Resources** − are special variables that hold references to resources external to PHP (such as database connections).




## Scope in PHP
PHP has 3 different variable scopes: global, local, static:
**Global**:
Variables used outside of a function will always have a global scope, they can be accessed inside and outside of functions.

**Local**:
Variables that are decelared within a function can only be accessed within the function. 

**Static**:
Once the value is set, the value does not change - however, the values can be accessed outside of the class without referancing the class first.




## Arrays 


## Loops


## Functions


## Conditionals (if statements)







## Forms

### GET 
The GET method sends the encoded user information appended to the page request. The page and the encoded information are separated by the `?` character.

Example URL showing a search funtion within www.bbc.co.uk, you can see the search terms after the `?` within the url
```
https://www.bbc.co.uk/search?q=sport
```

- The GET method produces a long string that appears in your server logs, in the browser's Location: box.
- The GET method is restricted to send upto 1024 characters only.
- Never use GET method if you have password or other sensitive information to be sent to the server.
- GET can't be used to send binary data, like images or word documents, to the server.
- The data sent by GET method can be accessed using QUERY_STRING environment variable.
- The PHP provides $_GET associative array to access all the sent information using GET method.


### POST
The POST method transfers information via HTTP headers (`<head>` parts in HTML). The information is encoded as described in case of GET method and put into a header called QUERY_STRING.

- The POST method does not have any restriction on data size to be sent.
- The POST method can be used to send ASCII as well as binary data.
- The data sent by POST method goes through HTTP header so security depends on HTTP protocol. By using Secure HTTP you can make sure that your information is secure.
- The PHP provides $_POST associative array (post data is sent using an assosiative array)to access all the sent information using POST method.


### Setting up a Form

Example form
```html
<form action="form.php" method="post">
   <input type="text" placeholder="Example Form textbox">
   <br>  
   <input type="text">
   <br>
   <input type="submit" name="submit">
</form>
```

We can check if the form works by running php code above the form: 
```php
// apache/nginx runs this code before rendering the below html
if(isset($_POST['submit'])) {
   echo "it works";
   echo $_POST;
}
```
The $_POST is what is known as a `superglobal`. This means that the variable is avalible in all scopes without the need to define the variable as a global.

### Extracting Infomation from a Form
To extract infomation from the, we can use the POST globalvariable along with referancing the name of the HTML form.

we can start by adding names to the HTML form. 
```HTML
<form action="form.php" method="post">
   <input type="text" name="username" placeholder="Enter Username">
   <br>  
   <input type="password" name="password" placeholder="Enter Password">
   <br>
   <input type="submit" name="submit">
</form>
```
This allows us to referance the form components in the future. 

We can then add the POST referancing in our php: 
```php
if(isset($_POST['submit'])) {
   echo "it works";
   echo $_POST;
   $username = $_POST['username']; // setting an array variable in POST to a variable on its own.
   $password = $_POST['password'];
   echo $username;
   echo $password;
}
?>
```

### Validating Form Data 
We can add simple validation by adding conditional statements. 

in our basic form, we can add some code to check the name length, and also add an array to simulate a database check:  
```php
if(isset($_POST['submit'])) {
   echo "it works";
   
   $minimun = 5;
   $names = array("homer", "marge", "bart", "lisa", "maggie");

   $username = $_POST['username'];
   $password = $_POST['password'];
   echo Hello . $username;
   echo "Your password is" . $password;

   //check if name is more that 5 letters 
   if(strlen($username) < $minimun ){
      echo "username has to be longer than 5 characters";
   }

   if(!in_array($username, $name)){
      echo "you are not allowed here";
   }
   else {
      echo "welcome";
   }
}
```

### External Page Submissions. 
We can send form data to external pages by changing the action of the form, so that it sends the user to a different page:
```html
<form action="form_process.php" method="post">
   <input type="text" name="username" placeholder="Enter Username">
   <br>  
   <input type="password" name="password" placeholder="Enter Password">
   <br>
   <input type="submit" name="submit">
</form>
```

In the new file `form_process.php` we can then modify the POST data that was send over from the `form.php` page. 
We can also move our php code from the form page into the `form_process.php` page 


form_process.php
```php
<?php

// apache/nginx runs this code before rendering the below html
if(isset($_POST['submit'])) {
   echo "it works";
   
   $minimun = 5;
   $names = array("homer", "marge", "bart", "lisa", "maggie");

   $username = $_POST['username'];
   $password = $_POST['password'];
   echo Hello . $username;
   echo "Your password is" . $password;

   //check if name is more that 5 letters 
   if(strlen($username) < $minimun ){
      echo "username has to be longer than 5 characters";
   }

   if(!in_array($username, $name)){
      echo "you are not allowed";
   }
   else {
      echo "welcome";
   }
}
?>
```

# Databases, SQL and PHP

## Installation of PHP and phpmyadmin

`link to LAMP stack documentation` 





## Setting up databases using SQL

## Setting up databases using phpmyadmin
Once phpmyadmin is set up, we can log in using the root account to see the existing databases within the mysql <contatiner/instance/server>? 

On the left hand side of the home page you can see a list of databases in the server, the layout is similar to a file browser, with the tables and colums set up like a collapsable directory. 

>**Note:** At the top of each 'folder' you can find the "new" tab - this allow you to create new databases/tables/columns

Example php myadmin explorer setup:
```
|Database 
---Table 
---|---Columns 
---|---|---|Indvidual Columns
---|---|---|---| Name (varchar)
               | Age (int)
               | Date of Birth (DATE)
               | Address (varchar)
```

## Setting up tables using phpmyadmin
We can set up tables in phpmyadmin by using the create table function - this should bring you to a interface that allows you to set the table name and column names. 
There are a variety of options for the table:  
**Name** - The name of the column  
**Type** - The type of data type (int/varchar etc)   
**Length/values** - The length of the data allowed in the database - if not set, will usually default to 256  
**Defaut** - The deafult value of the data (usefull if you dont want null values)  
**Collation** - The type of char set used by the data (usually set to `utf8mb4_general_ci`)  
**Attributes** - whether to set the data to a binary type or a timestamp     
**Null** - whether the data will allow null values (tick for yes)  
**A_I** - Auto Increment - the number will go up by one for each value, if checked you will not need to enter data in this column
**In_dex** - whether the column is a primary / foreign key  






### A Note on bootstrap
Bootsrtrap is a framwork that you can link to with its CSS and JS functions allowing for the quick development and deployment of front end UI elements for websites.
You can link using `href` functions to either the css or js using: 
```html
<!-- CSS only -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">

<!-- JS, Popper.js, and jQuery -->
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
```

## Setting up the frontend 

## Connecting to a database 
We can connect to an existing database using an inbuit api called `mysqli` 




Example connection script that can be imported/required into existing php scripts: 
```php
$servername='localhost';
$username='root';
$password='password';
$dbname = "crud";
$conn=mysqli_connect($servername,$username,$password,"$dbname");
if(!$conn){
   die('Could not Connect My Sql:' .mysql_error());
}
```
Alternate script to connect to database: 
```php
<?php
$connection = mysqli_connect('localhost','root','password','loginapp'); // parameters (ip/adress , username, password, database name)
   if($connection) {
      echo "We are connected <br>";
   }
   else{
      die("Database connection failed");
}
?>
```

## Creating data within php
We can create data by using the inbuilt `mysqli` functions to allow us to access and edit the database using SQL code which can be built and then sent to the database.
From the moment a user presses enter, a series of event occurs: 
 1. The data entered into the form is put into the `_POST` superglobal array 
 2. The `_POST` array is sent to the server 
 3. The username and password values are parsed out and assigned to induvidual varaibles
 4. The values are inserted into a SQL script 
 5. The sql script is passed to the mysql engine to run, inserting the data into the database. 



```php
<!-- php -->
<?php 
   if(isset($_POST['submit'])) {
      echo "yes";
      $_POST['submit'];

      $username = $_POST['username'];
      $password = $_POST['password'];

         // report back data (igonre security concernes for the moment)
         if($username && $password) {
            echo Hello . $username;
            echo "Your password is" . $password;
         }
         else{
            echo "Username or password is not set";
         }

      $connection = mysqli_connect('localhost','root','password','loginapp'); // parameters (ip/adress , username, password, database name)
            if($connection) {
               echo "We are connected <br>";
            }
            else{
               die("Database connection failed");
            }

            $query = "INSERT INTO users(username,password) ";
            $query .= "VALUES ('$username', '$password')"; // .= concatonates (adds on the end) onto existing values (same as += in js)


            $result = mysqli_query($connection, $query);// sends sql query to database 

            if(!$result){
               die("query failed" . mysqli_error());
            }
   }
?>
```

html
```html
<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
   </head>
   <body>
      <div class="col-sm-3">
         <form action="login_create.php" method="post">
            <div class="form-group">
               <label for="username">Username</label>
               <input type="text" name="username" class="form-control">
            </div>      
            <div class="form-group">
               <label for="password">Password</label>
               <input type="text" name="password" class="form-control">
            </div>     
            <input class="btn btn-primary"type="submit" name="submit" value="submit">
         </form>
      </div>

   </body>
</html>
```

## Reading Data with php 
We can read data from the database by using the same method as writing data - crafting and sending a SQL script to the server 

php
```php
<!-- php -->
<?php 

   $connection = mysqli_connect('localhost','root','password','loginapp'); // parameters (ip/adress , username, password, database name)
         if($connection) {
            echo "We are connected <br>";
         }
         else{
            die("Database connection failed");
         }

         $query = "SELECT * FROM users";
         


         $result = mysqli_query($connection, $query);// sends sql query to database 

         if(!$result){
            die("query failed" . mysqli_error());
         }

?>
```

html
```html
<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
   </head>
   <body>
      <div class="col-sm-3">
         
         <pre> <!--  preformatted text -->
         <?php
            while($row = mysqli_fetch_row($result)){
               print_r($row);
            }
         ?>
         </pre>

         <pre>
         <?php
            while($row = mysqli_fetch_assoc($result)){  // associative array
               print_r($row);
            }
         ?>
         </pre>
      
      </div>
   </body>
</html>
```

>**Note: Mysqli Functions**   
From: https://stackoverflow.com/questions/11480129/mysql-fetch-row-vs-mysql-fetch-assoc-vs-mysql-fetch-array  
All of the mentioned functions will return an array, the differences between them is what values that are being used as keys in the returned object.  
   ```mysql_fetch_row```: This function will return a row where the values will come in the order as they are defined in the SQL query, and the keys will span from 0 to one less than the number of columns selected.  
   ```mysql_fetch_assoc```: This function will return a row as an associative array where the column names will be the keys storing corresponding value.  
   ```mysql_fetch_array```: This function will actually return an array with both the contents of mysql_fetch_rowand mysql_fetch_assoc merged into one. It will both have numeric and string keys which will let you access your data in whatever way you'd find easiest.  
   
   It is recommended to use either _assoc or _row though.


## Updating Data 
We can update data by utilsing functions from both the creating and reading data - in the below example, we can select the id of the dataset to read the data based on the id. 

```php
include "db.php";
   $query = "SELECT * FROM users";

   $result = mysqli_query($connection, $query);// sends sql query to database 

   if(!$result){
      die("query failed" . mysqli_error($connection));
   }
```
```html
<?php 
include "db.php";
include "functions.php";

if(isset($_POST['submit'])) {
   $username = $_POST['username'];
   $password = $_POST['password'];
   $id = $_POST['id'];

   // building sql query 
   $query = "UPDATE users SET ";
   $query .= "username = '$username',";
   $query .= "password = '$password',";
   $query .= "WHERE id = '$id";

   echo $query;

   $result = mysqli_query($connection, $query);
   if(!$result) {
      die("Query failed" . mysqli_error($connection));
   }
}
?>

<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
   </head>
   <body>
      <div class="col-sm-3">
         <form action="" method="post">
            <div class="form-group">
               <label for="username">Username</label>
               <input type="text" name="username" class="form-control">
            </div>      
            <div class="form-group">
               <label for="password">Password</label>
               <input type="text" name="password" class="form-control">
            </div>   
            <div class="form-group">
            <select name="" id="">
               <?php
                  showAllData();
               ?>
            </select>
            </div>

            <input class="btn btn-primary"type="submit" name="submit" value="update">
         </form>
      </div>

   </body>
</html>
```


## Deleting Data
We modify the update rows functionality to just remove the row from the database, this code has already been refactored, so the delete row function is already inside `functions.php`  

functions.php
```php
function deleteRows() {
   global $connection; // alllows $connection to be used across db.php and functions.php

   $username = $_POST['username'];
   $password = $_POST['password'];
   $id = $_POST['id'];

   // building sql query 
   $query = "DELETE FROM users  ";
   $query .= "WHERE id = '$id' ";

   echo $query;

   $result = mysqli_query($connection, $query);
   if(!$result) {
      die("Query failed" . mysqli_error($connection));
   }
}
```

login_delete.php
```html
<?php 
include "db.php";
include "functions.php";

if(isset($_POST['submit'])) {
   deleteRows();
}
?>

<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
   </head>
   <body>
      <div class="col-sm-3">
         <form action="" method="post">
            <div class="form-group">
               <label for="username">Username</label>
               <input type="text" name="username" class="form-control">
            </div>      
            <div class="form-group">
               <label for="password">Password</label>
               <input type="text" name="password" class="form-control">
            </div>   
            <div class="form-group">
            <select name="id" id="">

               <?php
                  showAllData();
               ?>

               
            </select>
            </div>



            <input class="btn btn-primary"type="submit" name="submit" value="update">
         </form>
      </div>

   </body>
</html>

```





## Notes on refactoring code from a single file into seperate functions
With our current code, we have only been programming in a single file, while this is good for starting projects, this can very quickly spiral out of control.  

### Refactoring php code
With our login_update.php form, we can move the code that selects all the users into its own function.

```php
<?php
include "db.php";


function showAllData() {
// takes data from a database and displays certian rows based on the 'id' selected
   global $connection; // alllows $connection to be used across db.php and functions.php
   $query = "SELECT * FROM users";

   $result = mysqli_query($connection, $query);// sends sql query to database 

   if(!$result){
      die("query failed" . mysqli_error());
   }

   while($row = mysqli_fetch_assoc($result)){   // $row = fetch assosiative array of $result = query of 'SELECT * FROM users"
      $id = $row['id'];                         // fetch array of the id's in the database 
      echo "<option value=''>$id</option>";     // option value display the id's whithin the database
   } 
}
?>
```

within our `login_update` function we can now use the function:
```html
<?php 
include "db.php";
include "functions.php";
?>

<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
   </head>
   <body>
      <div class="col-sm-3">
         <form action="login_create.php" method="post">
            <div class="form-group">
               <label for="username">Username</label>
               <input type="text" name="username" class="form-control">
            </div>      
            <div class="form-group">
               <label for="password">Password</label>
               <input type="text" name="password" class="form-control">
            </div>   
            <div class="form-group">
            <select name="" id="">
               <?php
                  showAllData(); // uses the function from functions.php
               ?>
            </select>
            </div>



            <input class="btn btn-primary"type="submit" name="submit" value="update">
         </form>
      </div>

   </body>
</html>
```

### Refactoring HTML code
We can also refactor html code using the same php `include` statements, the below code includes a file that contains a header for some php code.

login_create.php
```php
include "includes/header.php";
```

includes/header.php
```html
<head>
   <meta charset="UTF-8">
   <Title>Create</Title>
   <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
</head>
```



## PHP Security
### SQL injection 
SQL injection is when someone enters code into an unprotected form by exiting the 'string' within the form. a good example of this is the heartbleed bug.

php has the function `mysqli_read_escape_string` which is a container that ecapsulates the form data. 

In the function `createRows()` it looks like this: 

without injectioon protection
```php
$username = $_POST['username'];
$password = $_POST['password'];
```

with injection protection
```php
$username = $_POST['username'];
$password = $_POST['password'];

$username = mysqli_real_escape_string($connection, $username);
$username = mysqli_real_escape_string($connection, $password);
```

### Password Encryption 
There are different types of encyption that are used, and most are change on a regular basis as new encyption methods are cracked or discovered.

Hashing and Salting


In our funcitons, we can add the encyption features to `createRows` to encypt the password that users give. 

```php
   $username = $_POST['username'];
   $password = $_POST['password'];

   $username = mysqli_real_escape_string($connection, $username);
   $username = mysqli_real_escape_string($connection, $password);

   $hashFormat = "$2y$10$";
   $salt = "iusesomecrazystrings";

   $hash_and_salt = $hashFormat . $salt;
   
   $password = crypt($password, $hash_and_salt);
```


## PHP and the Web

### GET superglobal 
`$_GET` is a superglobal varaible - it is avalible anywhere within a program. 

The GET method sends the encoded user information appended to the page request. The page and the encoded information are separated by the `?` character.

Example URL showing a search funtion within www.bbc.co.uk, you can see the search terms after the `?` within the url
```
https://www.bbc.co.uk/search?q=sport
```

- The GET method produces a long string that appears in your server logs, in the browser's Location: box.
- The GET method is restricted to send upto 1024 characters only.
- Never use GET method if you have password or other sensitive information to be sent to the server.
- GET can't be used to send binary data, like images or word documents, to the server.
- The data sent by GET method can be accessed using QUERY_STRING environment variable.
- The PHP provides $_GET associative array to access all the sent information using GET method.

We can also see this by writing a simple script `get.php`
```php
<?php 
   print_r($_GET) // print_r prints insides of array
?>
```
when we go to `get.php` we can see that it prints out an array 
when we go to `get.php?id=10` we can now see that the array has `id=10` inside of it.

To utilise `$_GET` we can use two methods: 
- Have a user write in the query string 
- send a link with query infomation in the string.

In almost all cases the latter is chosen, with a specific url being crafted to send the user to a custom page with the `$_GET` infomation avalible.

With the below example, we can make a link that sends a user to `get.php` with an id varaible se to 20 withinside the array.  

```html
<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
   </head>
   <body>
      <a href="get.php?id=20">get</a>

   </body>
</html>
```


### POST
The POST method transfers information via HTTP headers (`<head>` parts in HTML). The information is encoded as described in case of GET method and put into a header called QUERY_STRING.

- The POST method does not have any restriction on data size to be sent.
- The POST method can be used to send ASCII as well as binary data.
- The data sent by POST method goes through HTTP header so security depends on HTTP protocol. By using Secure HTTP you can make sure that your information is secure.
- The PHP provides $_POST associative array (post data is sent using an assosiative array)to access all the sent information using POST method.

With the below example, we can make a link that sends a user to `post.php` that shows how the function works.  

```html
<!-- php -->
<?php 
   echo $_POST['name']; // This code runs before the page html loads.
?>

<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
   </head>
   <body>
   <form action="post.php" method="post">
      <input name="name" type="text" placeholder="Example Form textbox">
      <br>  
      <input type="submit" name="submit">
   </form>
   </body>
</html>

```

The $_POST is what is known as a `superglobal`. This means that the variable is avalible in all scopes without the need to define the variable as a global.

When the form is submitted with data, the `$_POST` array now has a `name` variable value, which is then printed on the *reloaded* page as the form link is recursive.  

Using inspect element, we can see the http headers used 


## TDLR 
Both `GET` and `POST` are superglobals.  
Both use assosative arrays to send infomation.
`GET` sends infomation via the url. 
`POST` sends infomation via http headers.


## Cookies 
Cookies are a request for a browser to store a small file that can be used for storing and retreiving variables. 

### Setting cookies with php  
An example of a set cookie can be seen below in `cookie.php`:   
```php
   $name = "Homer";
   $value = 100;
   $experation = time() + (60 * 60 * 24 * 7 * 52) ; 
   // (unix time) + (use time functions to set cookie to expire in week)

   setcookie($name,$value,$experation);
```
when the user accesses the page, the cookie will be added to the users computer

### Reading cookies with php
An example of reading a cookie can be seen in `cookie.php`, note the if statment, a browser will continue looking for a cookie unless you tell it to stop.

```php
   // we know that the cookie is a assosative array, so we can find certian values 
   if(isset($_COOKIE["CookieExample"])) {
      $cookieExample = $_COOKIE["CookieExample"]; // pass the cookie data into a variable
      echo $cookieExample;
   } else {
      $cookieExample = "";
      echo "no cookie found";
   }
``` 

`cookie.php`
```html
<?php 
   $name = "CookieExample";
   $value = 100;
   $experation = time() + (60 * 60 * 24 * 7 * 52) ; //unix time + use time functions to set cookie to expire in week

   setcookie($name,$value,$experation);
?>

<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <title>Document</title>
   </head>
   <body>
      <?php
         // we know that the cookie is a assosative array, so we can find certian values 
         if(isset($_COOKIE["CookieExample"])) {
            $cookieExample = $_COOKIE["CookieExample"]; // pass the cookie data into a variable
            echo $cookieExample;
         } else {
            $cookieExample = "";
            echo "no cookie found";
         }
      ?>
   </body>
</html>
```

### Sessions 

















## Setting up a PHP + MySQL CRUD




### Requirements 
Web server 
PHP 

### Goals
Create MySQL Records 
Insert new records into the Contacts table.

Read MySQL Records
Reading MySQL records and display them in an HTML table.

Update MySQL Records
Update existing MySQL records in the Contacts table.

Delete MySQL Records  
Confirm and delete records from the Contacts table.

GET and POST Requests 
Send data to our app from an HTML form and URL parameters.

Prepared Statements 
Secure our SQL statements with prepared statements.


## Creating the database and setting up tables
We first need a database table that we can edit, unlike noSQL tables, a SQL table first has to be generated before someone can input data into the table. 

We need an:
- id
- name
- address 
- age

We can execute the following code to create a table named `contacts`: 


### Creating the database via a terminal
Entering mySQL via a terminal: `mysql -u root -p`
This will propmt you with a password, if entering with root 
 
Show all databases:  
`show databases;`

Create new database:  
`create database [database];`  

Select database:   
`use [database];`

Now we have access to the database that we need, we  can enter in the sql code. This can be achived either by:   
- pasting in the code into the command line.
- executing a file with the sql code inside. 

File `createDB.sql`
```sql
CREATE TABLE IF NOT EXISTS `contacts` (
	`id` int(11) NOT NULL AUTO_INCREMENT,
  	`name` varchar(255) NOT NULL,
  	`email` varchar(255) NOT NULL,
  	`phone` varchar(255) NOT NULL,
  	`created` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
	PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

we can run the above sql code using 
```sql
source <path_to_sql_file>/file.sql
```

for example: 
```sql
source /home/george/Documents/Programming/Projects/PHP/boilerplate/CRUD/createDB.sql
```

>**Note:** You can also  create the database using alternate methods such as generating it or importing the code into a database admin panel such as phpmyadmin.

### Inserting example data into the database 
We now have the database set up. The below code can add some example  data into our new database table:

```
INSERT INTO `contacts` (`id`, `name`, `email`, `phone`, `created`) VALUES
(1, 'Homer', 'homersimpson@example.com', '2026550143', '2019-05-08 17:32:00'),
(2, 'Marge', 'marge@example.com', '2025550121', '2019-05-08 17:28:44'),
(3, 'Bart', 'bart@example.com', '2004550121', '2019-05-08 17:29:27'),
(4, 'Ned', 'ned@example.com', '2022550178', '2019-05-08 17:29:27')
```

The above code adds 4 rows to the database. 




## Creating the application frontend 
The application can consist of 4 pages (this is an example, we can reformat it later):
- Navigation Page
- Creating Data
- Reading Data
- Updating Data
- Deleting Data

### Navigation Page 
We can use the navigation page to access other pages: 
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">

<head>
   <meta charset="utf-8"> <!-- defienes character types  -->
   <title>Title</title> <!-- Specifices a title for a document-->
   <link rel="stylesheet" href="index.css"> <!-- link to the css stylesheet-->
</head>

<body>
   <div class="content">

      <h1>CRUD Test Site </h1>

      <h2>HTML Forms</h2>

      <li><a href="insert.php"><strong>Create</strong></a> - add a user</li>
      <li><a href="read.php"><strong>Read</strong></a> - find a user</li>
      <li><a href="update.php"><strong>Update</strong></a> - edit a user</li>

      <h2>Database Scripts</h2>
      <li><a href="scripts/createDB.php"><strong>Create Database</strong></a> - create a database</li>
      <li><a href="scripts/createTable.php"><strong>Create Table</strong></a> - create a table</li>
   </div>
</body>

</html>
```

#### Creating a entry
We can use this page to insert new data into the database - this page includes a referance to input.php - a php script in a seperate file. 

insert.html
```html
<!DOCTYPE html>
<html>
  <body>
	<form method="post" action="scripts/insert.php">
		First name:<br>
		<input type="text" name="first_name">
		<br>
		Last name:<br>
		<input type="text" name="last_name">
		<br>
		City name:<br>
		<input type="text" name="city_name">
		<br>
		Email:<br>
		<input type="email" name="email">
		<br><br>
		<input type="submit" name="save" value="submit">
	</form>
  </body>
</html>
```

script.php
```php
<?php

// connections to php code 
$servername='localhost';
$username='root';
$password='password';
$dbname = "crud";
$conn=mysqli_connect($servername,$username,$password,"$dbname");
if(!$conn){
   die('Could not Connect My Sql:' .mysql_error());
}

//include_once 'config.php'; // connect to database
//require_once 'config.php'; // 

if(isset($_POST['save']))  // if the submit value 'save' is selected
{	 
   // select the variable from the form to post
   $first_name = $_POST['first_name']; // _POST is a superglobal array that contains avalible data 
   $last_name = $_POST['last_name'];
   $city_name = $_POST['city_name'];
   $email = $_POST['email'];

   echo $first_name . "<br>", $last_name . "<br>", $city_name . "<br>", $email . "<br>"; // (checking data for debug )

   // sql code to insert the form data
   $sql = "INSERT INTO Contacts (first_name, last_name, city_name, email) 
           VALUES ('$first_name','$last_name','$city_name','$email')";        // sql code to insert user data 



   // if (mysql (connects, run above sql code))
   if (mysqli_query($conn, $sql)) {
   echo "New record created successfully !";
   } 
   else {
      echo "Error: " . $sql . " " . mysqli_error($conn);
   }

   // Close connection
   mysqli_close($conn);
}
?>
```

### Reading Entries
