### Facts for Connecting to Database lesson:

`PHP Data Objects (PDO)` defines an interface in PHP to access certain databases

`PDO` class represents a connection between a database server and PHP.

`PDO_PGSQL` is a driver of `PHP Data Objects (PDO) Interface` that allows access between PHP and PostgreSQL database.

`PDO_PGSQL DSN` is the PostgreSQL data source name that carries the database parameters to establish a connection. It is composed of the following DSN parameters:

- `pgsql:` is the DSN prefix.
    
- `host` refers to the server’s hostname of the PostgreSQL database.

- `port` refers to the port number of the PostgreSQL database server.
    
- `dbname` is the database name.

- `user` refers to the username of the user.
    
- `password` refers to the password that is set by the `user`.

The example code below shows how PHP uses the `PDO_PGSQL` driver, `PDO_PGSQL DSN`, and `PDO` class to connect to the PostgreSQL database.

Code:

```php
<?php
    $host = 'localhost';
    $port = '5432';
    $db = 'MyDatabase';
    $username = 'postgres';
    $password = 'Admin01';
    
    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
        if ($conn) {
            echo "Successfully connected."; 
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection.";
    }
?>
```

- The database details `localhost`, `5432`, `MyDatabase`, `postgres`, and `Admin01` are assigned to the variables `$host`, `$port`, `$db`, `$username`, and `$password` respectively.

- `$dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";` the `PDO_PGQSL DSN` statement for connecting to the PostgreSQL database is assigned to the `$dsn` variable. The DSN parameters are separated with semicolons `;` and not spaces to follow the standard DSN delimiter to facilitate uniformity.

- The variables `$host`, `$port`, `$db`, `$username`, and `$password` are assigned to the DSN parameters `host`, `port`, `dbname`, `user`, and `password`.

- `$conn = new PDO($dsn)` creates the `$conn` object as an instance of the `PDO` class passing the argument `$dsn`.

- `if ($conn) { echo "Successfully connected."; }` evaluates the `$conn` object and executes the `echo` statement if `$conn` evaluates to true.

- The `try` block contains the statements that may throw a certain exception.

- The `catch` block executes the `echo` statement if an exception occurs within the `try` block.