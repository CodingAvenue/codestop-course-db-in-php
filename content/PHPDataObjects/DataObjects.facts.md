### Facts for PHP Data Objects lesson:

`PHP Data Objects (PDO)` defines an interface in PHP to access certain databases.

`PDO::query()` executes an SQL statement in a single function call and returns a result set as a `PDOStatement` object or `false` on failure.

The `PDOStatement` class represents a prepared statement and returns an associated result set after the statement is executed.

The example code below shows how to execute queries in PHP using `PDO::query()`.

```php
// Student.php
<?php
    require_once("Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "CREATE TABLE IF NOT EXISTS students (student_id SERIAL, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10), PRIMARY KEY (student_id))";

        $stmt = $conn->query($sql);
        if (!$stmt) {
            throw new Exception("Unable to create a table.");
        }
        echo "Successfully created a table."; 
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
- The `require_once("Connection.php");` statement includes the class `Connection.php` in the file `Student.php`.

- `$conn = Connection::getConnection()` assigns the return object in the `getConnection()` method from the `Connection` class to the `$conn` variable.

- `$sql = "CREATE TABLE IF NOT EXISTS students (student_id SERIAL, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10), PRIMARY KEY (student_id))";` assigns the SQL statement for creating a new table named `students` to the variable `$sql`.

- `$stmt = $conn->query($sql);` assigns the result set as a `PDOStatement` object to the variable `$stmt`.

- `if (!$stmt) { throw new Exception('Unable to create a table.'); }` evaluates the negated value of `$stmt` and throws an exception if `!$stmt` evaluates to `true`.

- `echo "Successfully created a table.";` displays the string `Successfully created a table.`.

- The `catch` block executes the `echo` statement if an exception occurs within the `try` block.
