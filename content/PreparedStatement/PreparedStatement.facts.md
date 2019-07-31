### Facts for Prepared Statement lesson:

`Prepared Statement` is a template for sending queries or uploading data to databases.

The `PDO::prepare()` method prepares an SQL statement for execution in the `PDOStatement::execute()` method and returns a statement object.

The `PDOStatement::execute()` method executes a prepared statement. 

The `PDOStatement::fetchAll()` method returns an array that holds all of the remaining rows in the result set.

The example code below shows how to prepare and execute an SQL statement using different parameter types in PHP.

1. `Positional placeholder parameters`

```php
$data = array (
    'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
    'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
);
        
$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birthdate, gender) VALUES (?,?,?,?)");
foreach ($data as $row) {
    $pstmt->execute($row);
}
```

- `$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birthdate, gender) VALUES (?,?,?,?)");` assigns the statement object of the `PDO::prepare()` method to the variable `$pstmt`.

- `VALUES (?,?,?,?)` specifies the values to be inserted using positional placeholder parameters `(?,?,?,?)`.

- The `foreach` statement iterates through each key in the array `$data`.

- `$pstmt->execute($row);` executes a prepared statement passing the argument `$row`.

2. `Named parameters`

```php
$data = array (
    'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
    'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
);

$sql = "INSERT INTO students (first_name, last_name, birthdate, gender) VALUES (:first_name, :last_name, :birthdate, :gender)";
$pstmt = $conn->prepare($sql);
foreach ($data as $sqldata => $values) {
        $pstmt->execute($values);
}
```

- `$sql = "INSERT INTO students (first_name, last_name, birthdate, gender) VALUES (:first_name, :last_name, :birthdate, :gender)";` assigns the SQL statement to the variable `$sql`.

- `VALUES (:first_name, :last_name, :birthdate, :gender)` specifies the values to be inserted using named parameters `:first_name`, `:last_name`, `:birthdate`, and `:gender`.

- `$conn->prepare($sql)` calls the `PDO::prepare()` method of the `$conn` object, executes the argument `$sql` and returns a statement object.

- `$pstmt = $conn->prepare($sql);` assigns the statement object to the variable `$pstmt`.

- The `foreach` statement iterates through each key of the array `$data`.

- `$pstmt->execute($values);` executes a prepared statement passing the argument `$values`.

