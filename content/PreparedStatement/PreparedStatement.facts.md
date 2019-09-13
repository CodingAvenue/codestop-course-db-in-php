### Facts for Prepared Statement lesson:

A `prepared statement` is used to compile an SQL statement once and executes multiple times with the same or different parameters. Parameters in a prepared statement can be substituted with `placeholders` which is helpful against SQL injection attacks.

- A `placeholder` is often indicated by a question mark `?` called `positional placeholder` or a colon followed by a variable name `:variable_name` called `named placeholder`.

- SQL injection `(SQLI)` is a code injection technique that alters SQL commands and exposes hidden data. It bypasses authentication then accesses, modifies, and deletes data in a database.

The execution of a prepared statement consists of using `prepare()` and `execute()` methods. 

- The `PDO::prepare()` method prepares an SQL statement for execution and returns a `PDOStatement` object.

- The `PDOStatement::execute()` method executes the prepared statement.

- The `PDOStatement::fetchAll()` method fetches all the result set rows.

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

- The `VALUES (?,?,?,?)` clause uses positional placeholders `?` to substitute the values to be inserted into the table to prevent SQL injections.

- The array keys `student1` and `student2` contain values to be inserted into the table. Positional placeholders require to order the key values in the same order of which the positional placeholders appear in the SQL statement.

- The first positional placeholder `?` is associated with the values `Berry` and `Vikki`, the second positional placeholder `?` is associated with the values `Meisner` and `Fernando`, the third positional placeholder `?` is associated with the values `2002-09-09` and `2005-05-17`, and the fourth positional placeholder is associated with the values `Male` and `Female`.

- The `foreach` statement iterates through each key in the multidimensional array `$data`.

- `$pstmt->execute($row);` executes a prepared statement passing the argument `$row` and returns the boolean value `true`.

2. Using `named placeholders`

```php
$data = array (
    ['first_name' => 'Berry', 'last_name' => 'Meisner', 'birth_date' => '2002-09-09', 'gender' => 'Male'],
    ['first_name' => 'Vikki', 'last_name' => 'Fernando', 'birth_date' => '2005-05-17', 'gender' => 'Female']
);

$sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (:first_name, :last_name, :birth_date, :gender)";
$pstmt = $conn->prepare($sql);
foreach ($data as $sqlData => $values) {
        $pstmt->execute($values);
}
```
- `$sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (:first_name, :last_name, :birth_date, :gender)";` assigns the SQL statement to the variable `$sql`.

- The `VALUES (:first_name, :last_name, :birth_date, :gender)` clause uses named placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender` to substitute the values to be inserted into the table to prevent SQL injections.

- The keys `first_name`, `last_name`, `birth_date`, and `gender` contain values to be inserted into the table. The keys should match the named placeholders specified in the SQL statement.

- `$pstmt = $conn->prepare($sql);` assigns the returned value of the `prepare()` method which is the `PDOStatement` object to the `$pstmt` variable.

- The `foreach` statement iterates through each key of the multidimensional array `$data`.

- `$pstmt->execute($values);` executes a prepared statement passing the argument `$values` and returns the boolean value `true`.