### Facts for Connecting to Database lesson:

`PDO_PGSQL` driver is a tool of `PHP Data Objects (PDO) Interface` to allow connection between PHP and PostgreSQL database.

`PDO` class represents a connection among PHP and a database server.

In the example code below shows how PHP uses the `PDO_PGSQL` driver and `PDO` class to connect to the PostgreSQL database.

Code:

```php
<?php
    $host='localhost';
    $port = '5432';
    $dbname = 'MyDatabase';
    $username = 'postgres';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try{
        $conn = new PDO($dsn);
        if($conn){
            echo "Connected to PostgreSQL with PDO"; 
        }
    }
    catch(Exception $e){
        echo "Unable to establish a connection";
    }
?>
```
Code breakdown:

- `"pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password"` uses the method `PDO_PGSQL Data Source Name (DSN)` to connect to the PostgreSQL database. It has the following elements:

    - `pgsql:` - It is the DSN prefix.
    
    - `host` - It is the server’s hostname of the PostgreSQL database.

    - `port` - It is the default port the PostgreSQL database server, which is `5432`.
    
    - `dbname` - It is the name that identifies the database.

    - `user` - It is the username that connects to the database name.
    
    - `password` - It is the password that is set by the `user`.

- `$conn = new PDO($dsn)` creates the `$conn` object which is an instance of the `PDO` class. The argument passed is `$dsn`.

- `$dsn` contains the `PDO_PGQSL DSN` statement that is required to connect to the PostgreSQL database.

- `if` statement evaluates the object `$conn`. 

- `try-catch` statement handles any exceptions if any error occurs.

- `catch` block displays the error message `Unable to establish a connection` if there is a problem with the connection.