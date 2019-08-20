### Facts for Prepared Statement lesson:

A `prepared statement` is used to execute an SQL statement multiple times with the same or different parameter values. The execution of a prepared statement consists of using `prepare()` and `execute()` methods. 

- The `PDO::prepare()` method prepares an SQL statement for execution using the `PDOStatement::execute()` method and returns a `PDOStatement` object.

- The `PDOStatement::execute()` method executes a prepared statement and returns `true` on success or `false` on failure.

- The `PDOStatement::fetchAll()` method fetches a result set and returns an array of the remaining rows in a result set.

Using `placeholders` instead of actual parameter values in a prepared statement is useful against SQL injection attacks because `placeholders` substitute the actual input values in an SQL statement. A `placeholder` is often indicated by a question mark `?` called `positional placeholder` or a colon followed by a variable name `:variable_name` called `named placeholder`. 

SQL injection `(SQLI)` is a code injection technique that alters SQL commands and exposes hidden data. It could bypass authentication then accesses, modifies, and deletes data in a database. 

The example code below shows how to prepare and execute an SQL statement using different types of placeholder in PHP.

1. Using `positional placeholders`

```php
$data = array (
    'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
    'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
);
        
$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)");
foreach ($data as $row) {
    $pstmt->execute($row);
}
```
- `$conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)")` prepares the SQL statement.

- `$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)");` assigns the returned value of the `prepare()` method which is the `PDOStatement` object to the `$pstmt` variable.

- The `VALUES (?,?,?,?)` clause uses positional placeholders `?,?,?,?` to substitute the values to be inserted into the table to prevent SQL injections.

- The `foreach` statement iterates through each key in the multidimensional array `$data`.

- `$pstmt->execute($row);` executes a prepared statement passing the argument `$row`.

2. Using `named placeholders`

```php
$data = array (
    'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
    'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
);

$sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (:first_name, :last_name, :birth_date, :gender)";
$pstmt = $conn->prepare($sql);
foreach ($data as $sqlData => $values) {
        $pstmt->execute($values);
}
```
- `$sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (:first_name, :last_name, :birth_date, :gender)";` assigns the SQL statement to the variable `$sql`.

- The `VALUES (:first_name, :last_name, :birth_date, :gender)` clause uses named placeholders `:first_name, :last_name, :birth_date, :gender` to substitute the values to be inserted into the table to prevent SQL injections.

- `$pstmt = $conn->prepare($sql);` assigns the returned value of the `prepare()` method which is the `PDOStatement` object to the `$pstmt` variable.

- The `foreach` statement iterates through each key of the multidimensional array `$data`.

- `$pstmt->execute($values);` executes a prepared statement passing the argument `$values`.