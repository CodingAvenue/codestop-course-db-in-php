### Facts for PHP Data Objects lesson:

`PHP Data Objects (PDO)` defines an interface in PHP to access certain databases.

`PDO::query()` executes an SQL statement, returns a `PDOStatement` object or on failure a `false` boolean value.

`PDOStatement` class represents a prepared statement, executes the statement and returns an associated result set.

The example code below shows how to execute queries in PHP using `PDO::query()`.

```php
// student.php
<?php
    require_once ("connection.php");

    $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, firstname VARCHAR(80), lastname VARCHAR(80), birthdate DATE, gender VARCHAR(10))";
    
    try {
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
- The `require_once ("connection.php");` statement includes the file `connection.php` in the file `student.php`.

- `$sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, firstname VARCHAR(80), lastname VARCHAR(80), birthdate DATE, gender VARCHAR(10))";` the SQL statement for creating a new table named `students` is assigned to the variable `$sql`.

- `$stmt = $conn->query($sql);` executes the argument `$sql` in the `query()` method of the `$conn` object and stores the result set a `PDOStatement` object to the variable `$stmt`.

- `if (!$stmt) { throw new Exception('Unable to create a table.'); }` evaluates the `$stmt` object. If the statement evaluates to `false`, it throws an exception.

- The statement `echo "Successfully created a table."; ` is executed if the `if` statement evaluates to `true`.

- The `catch` block executes the `getMessage()` function and returns the `Exception` message if an exception occurs within the `try` block 