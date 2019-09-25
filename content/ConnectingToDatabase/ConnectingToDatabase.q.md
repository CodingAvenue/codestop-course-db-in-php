# Connecting to Database

+++

### Part 1: Sample Code Analysis

:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
/// type=SS, answer=[3]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `"Successfully connected!"`.

- It prints `Unable to establish a connection.`.


/// type=SS, answer=[3]

On line 2, what is `$host`?

- It is a string.

- It is a function.

- It is a variable.

- It is a statement.

- It is an operator.


/// type=SS, answer=[3]

In the statement `$host='localhost';` on line 2, what is `localhost`?

- It is the DSN prefix.

- It is the name of the database.

- It is the server’s hostname of the PostgreSQL database.

- It is the port number of the PostgreSQL database server.

- It is the username of the user that will be used to connect to the database.


/// type=SS, answer=[5]

In the statement `$dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";`, what is `pgsql:`?

- It is the object.

- It is the `PDO` class.

- It is the username.

- It is the hostname.

- It is the DSN prefix.


/// type=SS, answer=[1]

Which variable contains the value of the database name?

- `$db`

- `$dsn`

- `$port`

- `$host`

- `$username`


/// type=SS, answer=[4]

In the statement `$dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";`, what does `host=$host;` do?

- It identifies the hostname of the DSN parameter.

- It relocates the DSN parameter `host` to the variable `$host`.

- It transfers the value of the `$host` variable to the DSN parameter `host`.

- It assigns the `$host` variable containing the value `localhost` to the DSN parameter `host`. 

- It creates the `$host` variable containing the value `localhost` to the DSN parameter `host`.


/// type=SS, answer=[4]

Which variable contains the value of the database server's hostname?

- `$db`

- `$dsn`

- `$port`

- `$host`

- `$username`


/// type=SS, answer=[5]

In the statement `$dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";`, what does `user=$username;` do?

- It identifies the username of the DSN parameter.

- It relocates the DSN parameter `user` to the variable `$username`.

- It transfers the value of the `$username` variable to the DSN parameter `user`.

- It creates the `$host` variable containing the value `localhost` to the DSN parameter `user`.

- It assigns the `$username` variable containing the value `codestop` to the DSN parameter `user`. 


/// type=SS, answer=[5]

What is the name of the database?

- `5432`

- `Admin01`

- `codestop`

- `localhost`

- `MyDatabase`


/// type=SS, answer=[5]

On line 4, what is `5432`?

- It is the password.

- It is the DSN prefix.

- It is the database name.

- It is the server’s hostname of the PostgreSQL database.

- It is the default port number of the PostgreSQL database.


/// type=SS, answer=[5]

In the statement `$dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";`, what does `$dsn` do?

- It creates the object.

- It holds the user's password.

- It contains the database name.

- It stores the `pgsql:` DSN prefix.

- It holds the `PDO_PGQSL DSN` statement.


/// type=SS, answer=[5]

Which of the following is an object?

- `$db`

- `new`

- `$dsn`

- `$host`

- `$conn`


/// type=MS, answer=[4,5]

Which statements correctly describe the code on line 11?

- It assigns `PDO($dsn)` to `$conn`.

- It sets the value of `$dsn` to `PDO()`.

- It evaluates the `$conn` object of the `PDO` class.

- It creates the `$conn` object as an instance of the `PDO` class.

- It passes the `$dsn` variable as an argument of the `PDO` class.


/// type=SS, answer=[5]

What does the `if` construct do on line 12?

- It adds the value of `$conn`.

- It displays the value of `$conn`.

- It removes the value of `$conn`.

- It assigns a value to the `$conn` variable.

- It evaluates the `$conn` object inside the parentheses `()`.


/// type=MS, answer=[2,4]

Which statements correctly describe the code on lines 12, 13, and 14?

- The statement displays the value assigned to the `$conn` variable.

- The `if` statement evaluates to `true` and the `echo` statement on line 13 is executed.

- The `if` statement evaluates to `false` and the `echo` statement on line 13 is not executed.

- The `if` statement evaluates to `true` and it displays the string `"Successfully connected!"`.

- The `if` statement evaluates to `false` and it displays the string `Unable to establish a connection.`.

:::


:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'LibraryDb';
    $port = '5432';
    $username = 'codestop';
    $password = 'adminPwd01';
    
    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
/// type=SS, answer=[3]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `"Successfully connected!"`.

- It prints `Unable to establish a connection.`.


/// type=MS, answer=[1,5]

Which of the following are classes?

- `PDO`

- `$host`

- `$conn`

- `pgsql:`

- `Exception`


/// type=SS, answer=[4]

Which statement correctly describes the code on lines 13, 14, and 15?

-  It creates the `$e` object.

- It evaluates the `if` statement.

- It throws the value of the `$conn` object.

- It executes the `echo` statement if an exception occurs within the `try` block.

- It displays the string `Unable to establish a connection.` if the `if` statement evaluates to `true`.


/// type=MS, answer=[4,5]

Which statements correctly describe the code on line 9?

- It evaluates the `$conn` object.

- It sets the `PDO` class to the `PDO_PGQSL DSN` statement

- It assigns the `PDO_PGQSL DSN` statement to the `PDO` class.

- It creates the `$conn` object as an instance of the `PDO` class.

- It passes the `PDO_PGQSL DSN` statement as an argument of the `PDO` class.


:::


+++


+++

### Part 2: Knowledge Assessment

/// type=SS, answer=[5]

Which statement best describes `PDO_PGSQL`?

- It is a method that copies data from a file into the table.

- It is a method that copies data from the database table into a PHP array.

- It is a driver of `PHP Data Objects Interface` that allows access from PHP to MS SQL server.

- It is a driver of `PHP Data Objects Interface` that allows access from PHP to MySQL databases.

- It is a driver of `PHP Data Objects Interface` that allows access from PHP to PostgreSQL databases.


/// type=MS, answer=[1,2,3,4]

Which of the following are `PDO_PGSQL Data Source Name (DSN)` parameters?

- `host`

- `port`

- `user`

- `pgsql:`

- `databaseName`


/// type=SS, answer=[5]

Which DSN parameter holds the name of the database?

- `db`

- `host`

- `port`

- `pgsql:`

- `dbname`


/// type=SS, answer=[2]

Which DSN parameter holds the name of the user?

- `name`

- `user`

- `host`

- `dbname`

- `username`


/// type=SS, answer=[5]

Which statement best describes a `PDO` class?

- It handles an exception if any error occurs.

- It evaluates the connection in a PHP application.

- It sets the parameters between PHP and a database server.

- It allows an unstable connection between PHP and a database.

- It represents a connection between a database server and PHP.


+++


+++

### Part 3: Finding and Fixing Errors

:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `"Successfully connected!"`.

- It prints `Unable to establish a connection.`.


/// type=MS, answer=[2,4]

Which statements correctly describe the error?

- There is no semicolon `;` at the end of the statement on line 8.

- There is no `psql:` DSN prefix specified in the statement on line 8.

- The statement `$conn = new PDO($dsn);` on line 11, the argument passed is `$dsn`.

- On line 8, the statement `$dsn = "host=$host;port=$port;dbname=$db;user=$username;password=$password";` is incorrect.

- There are no parentheses `()` that enclosed the statement `host=$host;port=$port;dbname=$db;user=$username;password=$password;` on line 8.

:::


/// type=CR, answer=[tests/ConnectingToDatabase/MissingDSNPrefixTest.php]

Correct the code so that it outputs the string `Successfully connected!`.

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```


:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = PDO($dsn);
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
/// type=SS, answer=[4]

Execute the program. What is the error message?

- Unable to establish a connection.

- Undefined variable: `dsn` on line 11

- Undefined variable: `conn` on line 12

- Uncaught Error: Call to undefined function `PDO()` on line 11

- Uncaught ArgumentCountError: `PDO::__construct()` expects at least `1` parameter, `0` given on line 11


/// type=MS, answer=[3,4]

Which statements correctly describe the error?

- On line 11, the variable name `$conn` is invalid.

- The `$dsn` variable is passed as an argument on line 11.

- There is no `new` keyword between `=` and `PDO` on line 11.

- On line 11, the statement `$conn = PDO($dsn);` is incorrect.

- There is a semicolon `;` after the statement `$conn = PDO($dsn)` on line 11.

:::


/// type=CR, answer=[tests/ConnectingToDatabase/MissingNewKeywordTest.php]

Correct the code so that it outputs the string `Successfully connected!`.

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = PDO($dsn);
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```


:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=;port=;dbname=;user=;password=";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Successfully connected!";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }   
?>
```
/// type=SS, answer=[4]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `Unable to establish a connection.`.

- It prints `"Unable to establish a connection."`.


/// type=MS, answer=[2,3]

Which statements correctly describe the error?

- On line 8, the variable name `$conn` variable is invalid.

- There are no values assigned to the required DSN parameters on line 8.

- On line 8, the statement `$dsn = "pgsql:host=;port=;dbname=;user=;password=";` is incorrect.

- The statement `$dsn = "pgsql:host=;port=;dbname=;user=;password=";` is written outside the `if` statement.

- There are no parentheses `()` that enclosed the statement `$dsn = "pgsql:host=;port=;dbname=;user=;password=";` on line 8.

:::


/// type=CR, answer=[tests/ConnectingToDatabase/MissingAssignedVariablesTest.php]

Correct the code so that it outputs the string `Successfully connected!`.

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=;port=;dbname=;user=;password=";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Successfully connected!";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }     
?>
```


:::

/// type=REPL

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';
    
    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
/// type=SS, answer=[3]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `"Successfully connected!"`.

- It prints `Unable to establish a connection.`.


/// type=MS, answer=[2,3]

On line 3, remove the statement `$db = 'MyDatabase';`. Execute the program. What are the error messages?

- Undefined variable: `db` on line 4

- Undefined variable: `db` on line 9

- Unable to establish a connection.

- Undefined variable: `conn` on line 13

- syntax error, unexpected `=`, expecting end of file on line 9

:::


:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'newhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
/// type=SS, answer=[4]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `Unable to establish a connection.`.

- It prints `"Unable to establish a connection."`.


/// type=SS, answer=[3]

Which statement correctly describes the error?

- There is no `psql:` DSN prefix on line 9.

- On line 9, the DSN parameters are separated with semicolons `;`.

- The database server's hostname `newhost` on line 2 is incorrect.

- There is no open curly brace `{` after the `if` statement on line 10.

- On line 9, the command `"pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password"` is passed as an argument.

:::


/// type=CR, answer=[tests/ConnectingToDatabase/IncorrectHostNameTest.php]

Correct the code so that it outputs the string `Successfully connected!`. Hint: Use `localhost` as the database server’s hostname.

```php
<?php
    $host = 'newhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'codestop';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected!"; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```


:::

/// type=REPL

```php
<?php
   $host = 'localhost';
   $db = 'MyDatabase';
   $port = '5432';
   $username = 'codestop';
   $password = 'Admin01';
   
   $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

   try {
       $conn = new PDO($dsn);
       if ($conn) {
           echo "Successfully connected!";
       }
   } catch (Exception $e) {
       echo "Unable to establish a connection.";
   }
?>
```
/// type=SS, answer=[3]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `"Successfully connected!"`.

- It prints `Unable to establish a connection.`.


/// type=SS, answer=[4]

On line 4, replace the value `5432` with `1234`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `Unable to establish a connection.`.

- It prints `"Unable to establish a connection."`.


/// type=MS, answer=[1,3]

Which statements correctly describe the error?

- The specified port number `1234` is incorrect.

- The value `1234` is enclosed in single quotes `''`.

- The port number `1234` is not where the database server currently runs.

- There are no parentheses `()` that enclosed the statement `$port = '5432';`.

- The statement `$port = '5432';` is written after the statement `$db = 'MyDatabase';`

:::


+++


+++

### Part 4: Practice

/// type=CR, answer=[tests/ConnectingToDatabase/CreatePHPApplicationConnectingToPostgreSQLTest.php]

Write a PHP program that uses the `PDO_PGSQL DSN` and `PDO` class to connect to the PostgreSQL database. First, create the variables `$host`, `$db`, `$port`, `$username`, and `$password`. Assign the values `localhost`, `MyDatabase`, `5432`, `codestop`, and `Admin01` to the variables respectively. Then, assign the `PDO_PGSQL DSN` statement which contains the DSN parameters `host`, `port`, `dbname`, `username`, and `password` to the `$dsn` variable. Set the DSN parameters with their respective values `$host`, `$db`, `$port`, `$username`, and `$password`. Next, add the `try` and `catch` statements. Inside the `try` block, add a statement that creates the `$conn` object an instance of the `PDO` class which passes the argument `$dsn`. Then, add the `if` statement to evaluate the `$conn` object inside the parentheses `()`. Inside the `if` block, add an `echo` statement to display the string `Successfully connected!`. Inside the `catch` block, add an `echo` statement to display the error message `Unable to establish a connection.` if an exception occurs within the `try` block. Run the program to view the output.

```php
<?php


?>
```

+++