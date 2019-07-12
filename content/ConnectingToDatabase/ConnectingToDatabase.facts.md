### Facts for Connecting to Database lesson:

`PDO` class represents a connection between PHP and a database server.

`PDO_PGSQL` is a driver of `PHP Data Objects (PDO) Interface` that allows access between PHP and PostgreSQL database.

`PDO_PGSQL DSN` is the PostgreSQL data souce name that carries the database parameters in order to connect. It is composed of the following DSN parameters:

- `pgsql:` is the DSN prefix.
    
- `host` refers to the server’s hostname of the PostgreSQL database.

- `port` refers to the port number of the PostgreSQL database server.
    
- `dbname` refers to the name of the database.

- `user` refers to the username of the user.
    
- `password` refers to the password that is set by the `user`.

In the example code below shows how PHP uses the `PDO_PGSQL` driver, `PDO_PGSQL DSN`, and `PDO` class to connect to the PostgreSQL database.

Code:

```php
<?php
    $host = 'localhost';
    $port = '5432';
    $dbname = 'MyDatabase';
    $username = 'postgres';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Connected to PostgreSQL with PDO."; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```
Code breakdown:

- `"pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password"` carries the variables of the DSN parameters connecting to the PostgreSQL database.

- `$dsn` contains the `PDO_PGQSL DSN` statement that is required to connect to the PostgreSQL database.

- `$conn = new PDO($dsn)` creates the `$conn` object which is an instance of the `PDO` class passing the argument `$dsn`.

- `if` statement evaluates the `$conn` object. 

- `try` block evaluates the `if` statement that may throw an exception if any error occurs.

- `catch` block displays the error message `Unable to establish a connection.` if there is a problem with the connection.