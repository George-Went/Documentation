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

## Databases, SQL and PHP

### Installation of PHP and phpmyadmin

`link to LAMP stack documentation` 





### Setting up databases using SQL

### Setting up databases using phpmyadmin
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

### A Note on bootstrap
Bootsrtrap is a framwork that you can link to with its CSS and JS functions allowing for the quick development and deployment of front end UI elements for websites.
















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
   <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>

<div class="topnav" id="myTopnav">
   <a href="/public/index.html">Home</a>
   <a href="/public/js_examples.html">JS Examples</a>
   <a href="/phpExamples/php_examples.php">PHP Examples</a>
   <a href="/CRUD/index.php" class="active">CRUD</a>
   <a href="javascript:void(0);" class="icon" onclick="navbarFunction()">
      <i class="fa fa-bars"></i>
   </a>
</div>

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









