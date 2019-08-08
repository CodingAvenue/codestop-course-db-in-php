### Facts for Prepared Statement lesson:

Using `prepared statements` in executing the same SQL statement repeatedly helps against SQL injections. It contains `placeholders` instead of actual parameter values during execution which is useful against SQL injection attacks. Execution of a prepared statement consists of using `prepare()` and `execute()` methods.

SQL injection `(SQLI)` is a code injection technique that alters SQL commands and exposes hidden data. It could bypass authentication then accesses, modifies and deletes data in a database. 

- The `PDO::prepare()` method prepares an SQL statement for execution using the `PDOStatement::execute()` method and returns a `PDOStatement` object.

- The `PDOStatement::execute()` method executes a prepared statement and returns `true` on success or `false` on failure.

- The `PDOStatement::fetchAll()` method fetches large result sets and returns either an array containing the remaining rows in the result set or an empty array.

`Placeholders` are used to substitute the input values during runtime to protect against SQL injection. A `placeholder` is often indicated by a question mark `?` called `positional placeholder` or a colon followed by a variable name `:variable_name` called `named placeholder`. 

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

- `$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)");` assigns the `PDOStatement` object of the `prepare()` method to the variable `$pstmt`.

- `(?,?,?,?)` substitutes the values to be inserted in the SQL statement using four positional placeholders `?,?,?,?` for four input values to prevent from SQL injections.

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

- `(:first_name, :last_name, :birth_date, :gender)` substitutes the values to be inserted in the SQL statement using named placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender` to prevent from SQL injections.

- `$pstmt = $conn->prepare($sql);` assigns the `PDOStatement` object of the `prepare()` method to the `$pstmt` variable.

- The `foreach` statement iterates through each key of the multidimensional array `$data`.

- `$pstmt->execute($values);` executes a prepared statement passing the argument `$values`.