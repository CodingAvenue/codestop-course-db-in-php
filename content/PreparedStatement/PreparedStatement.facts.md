### Facts for Prepared Statement lesson:

`Prepared statement` is used to execute the same statement with high efficiency repeatedly. Execution of a prepared statement consists of using `prepare()` and `execute()` methods which help to prevent SQL injection attacks.

- The `PDO::prepare()` method prepares an SQL statement for execution using the `PDOStatement::execute()` method and returns a `PDOStatement` object.

- The `PDOStatement::execute()` method executes a prepared statement and returns `true` on success or `false` on failure.

- The `PDOStatement::fetchAll()` method returns an array which contains the result set of the remaining rows.

It is often beneficial to use `placeholders` to substitute the input values during runtime to protect against SQL injection. A `placeholder` is often indicated by a question mark `?` or a colon followed by a variable name `:variable_name`. These are called `positional placeholders` and `named placeholders` respectively.

The example code below shows how to prepare and execute an SQL statement using different placeholder types in PHP.

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

- `(?,?,?,?)` substitutes the values to be inserted in the SQL statement using four question marks `?,?,?,?` for four input values to prevent from SQL injections.

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

- `$conn->prepare($sql)` calls the `prepare()` method of the `$conn` object, executes the argument `$sql` and returns a statement object.

- `$pstmt = $conn->prepare($sql);` assigns the `PDOStatement` object to the variable `$pstmt`.

- The `foreach` statement iterates through each key of the multidimensional array `$data`.

- `$pstmt->execute($values);` executes a prepared statement passing the argument `$values`.

