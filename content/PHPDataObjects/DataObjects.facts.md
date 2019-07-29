### Facts for PHP Data Objects lesson:

`PHP Data Objects (PDO)` defines an interface in PHP to access certain databases.

`PDO::query()` executes an SQL statement in a single function call and returns a result set as a `PDOStatement` object or `false` on failure.

The `PDOStatement` class represents a prepared statement and returns an associated result set after the statement is executed.

The example code below shows how to execute queries in PHP using `PDO::query()`.

```php
// student.php
<?php
    require_once("connection.php");

    $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";
    
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
- The `require_once("connection.php");` statement includes the file `connection.php` in the file `student.php`.

- `$sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";` assigns the SQL statement for creating a new table named `students` to the variable `$sql`.

- `$stmt = $conn->query($sql);` assigns the result set as a `PDOStatement` object to the variable `$stmt`.

- `if (!$stmt) { throw new Exception('Unable to create a table.'); }` evaluates the negated value of `$stmt` and throws an exception if `!$stmt` evaluates to `true`.

- `echo "Successfully created a table.";` displays the string `Successfully created a table.` inside the `try` block.

-  The `catch` block executes the `echo` statement if an exception occurs within the `try` block.
