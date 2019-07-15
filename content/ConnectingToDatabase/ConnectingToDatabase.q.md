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
    $username = 'postgres';
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


/// type=SS, answer=[4]

In the statement `$host='localhost';` on line 2, what is `localhost`?

- It is the DSN prefix.

- It is the name of the database.

- It is the username of the user.

- It is the server’s hostname of the PostgreSQL database.

- It is the port number of the PostgreSQL database server.


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

Which variable contains the value of the database server's hostname?

- `$db`

- `$dsn`

- `$port`

- `$host`

- `$username`


/// type=SS, answer=[5]

What is the name of the database?

- `5432`

- `Admin01`

- `postgres`

- `localhost`

- `MyDatabase`


/// type=SS, answer=[5]

On line 4, what is `5432`?

- It is the password.

- It is the DSN prefix.

- It is the database name.

- It is the server’s hostname of the PostgreSQL database.

- It is the port number where the PostgreSQL database server runs.


/// type=SS, answer=[5]

In the statement `$dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";`, what does `$dsn` do?

- It creates the object.

- It holds the value of the user's password.

- It contains the value of the database name.

- It stores the value of the DSN prefix `pgsql:`.

- It holds the value of the `PDO_PGQSL DSN` statement.


/// type=SS, answer=[4]

Which of the following is an object?

- `new`

- `$dsn`

- `$host`

- `$conn`

- `$dbname`


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

Which statements correctly describe the code on line 12?

- The statement displays the value assigned to the `$conn` variable.

- The `if` statement evaluates to `true` and the `echo` statement on line 14 is executed.

- The `if` statement evaluates to `false` and the `echo` statement on line 14 is not executed.

- The `if` statement evaluates to `true` and it displays the string `"Successfully connected!"`.

- The `if` statement evaluates to `false` and it displays the string `Unable to establish a connection.`.

:::


:::

/// type=REPL, readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'postgres';
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


/// type=MS, answer=[1,5]

Which of the following are classes?

- `PDO`

- `$host`

- `$conn`

- `pgsql:`

- `Exception`


/// type=MS, answer=[3,4]

Which statements correctly describe the code on line 13?

- It evaluates the `if` statement.

- It throws the value of the `$conn` object.

- It creates the `$e` object containing the exception information.

- It retrieves an exception if an exception occurs within the `try` block.

- It displays the string `Unable to establish connection.` if the `if` statement evaluates to `true`.


:::


+++


+++

### Part 2: Knowledge Assessment

/// type=SS, answer=[5]

Which statement best describes `PDO_PGSQL`?

- It is a method that copies data from a file into the table.

- It is a method that copies data from the database table into PHP array.

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

- It allows unstable connection between PHP and a database.

- It signifies a connection between a database server and PHP.


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
    $username = 'postgres';
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


/// type=MS, answer=[1,4]

Which statements correctly describe the error?

- There is no DSN prefix `psql:` on line 8.

- There is no semicolon `;` at the end of the statement on line 8.

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
    $username = 'postgres';
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
    $username = 'postgres';
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

- The `$conn` variable is an invalid variable name.

- The `$dsn` variable is inside the parentheses `()`.

- There is no `new` keyword between `=` and `PDO` on line 11.

- On line 11, the statement `$conn = PDO($dsn);` is incorrect.

- There is a semicolon `;` after the statement `$conn = PDO($dsn)`.

:::


/// type=CR, answer=[tests/ConnectingToDatabase/MissingNewKeywordTest.php]

Correct the code so that it outputs the string `Successfully connected!`.

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'postgres';
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

/// type=REPL readonly=true

```php
<?php
    $host = 'localhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'postgres';
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

- On line 8, the `$dsn` variable is an invalid variable name.

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
    $username = 'postgres';
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
    $username = 'postgres';
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

On line 2, remove the statement `$db = 'MyDatabase';`. Execute the program. What are the error messages?

- Undefine variable: `db` on line 4

- Undefined variable: `db` on line 9

- Unable to establish a connection.

- Undefined variable: `conn` on line 13

- syntax error, unexpected `=`, expecting end of file on line 9

:::


:::

/// type=REPL readonly=true

```php
<?php
    $host = 'newhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'postgres';
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

- There is no DSN prefix `psql:` on line 9.

- On line 9, the DSN parameters are separated by a semicolon `;`.

- The database server's hostname `newhost` on line 1 is incorrect.

- There is no open curly brace `{` after the `if` statement on line 10.

- On line 9, the command `"pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password"` is passed as an argument.

:::


/// type=CR, answer=[tests/ConnectingToDatabase/IncorrectHostNameTest.php]

Correct the code so that it outputs the string `Successfully connected!` using its database server’s hostname as `localhost`.

```php
<?php
    $host = 'newhost';
    $db = 'MyDatabase';
    $port = '5432';
    $username = 'postgres';
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
   $username = 'postgres';
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

On line 4, replace the string value `5432` with `1234`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Successfully connected!`.

- It prints `Unable to establish a connection.`.

- It prints `"Unable to establish a connection."`.


+++


+++

### Part 4: Practice

/// type=CR, answer=[tests/ConnectingToDatabase/CreatePHPApplicationConnectingToPostgreSQLTest.php]

Write a PHP program that uses the `PDO_PGSQL` driver, `PDO_PGSQL DSN`, and `PDO` class to connect to the PostgreSQL database. First, create the following variables `$host`, `$db`, `$port`, `$username`, and `$password`. Assign the values `localhost`, `MyDatabase`, `5432`, `postgres`, and `Admin01` respectively to the variables. Then, assign the `PDO_PGSQL DSN` statement which contains the DSN parameters `host`, `port`, `dbname`, `username`, and `password` to the `$dsn` variable. Set the DSN parameters with their respective variables `$host`, `$db`, `$port`, `$username`, and `$password`. Next, create the `try` block which contains two statements. In the first statement, create the `$conn` object an instance of the `PDO` class which passes the argument `$dsn`. In the second statement, write the `if` statement to evaluate the `$conn` object inside the parentheses `()`. If the expression evaluates to `true` then, the `echo` statement displays the string `Successfully connected!`. Set the `catch` block to retrieve the exception if an exception occurs within the `try` block. Create the `$e` object an instance of the `Exception` class. Then, display the error message `Unable to establish a connection.` inside the `catch` block. Run the program to view the output.

```php
<?php


?>
```

+++