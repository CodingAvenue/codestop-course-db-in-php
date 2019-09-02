### Facts for Prepared Statement with Binding Methods

Parameter binding in a prepared statement is essential against SQL injections. The `bindValue()` and `bindParam()` methods bind variables or values in a prepared statement that contains placeholders as parameters such as a positional placeholder `?` or named placeholder `:variable_name`.

- `PDOStatement::bindValue()` method binds a value or variable to a parameter. It passes both `value` and `variable`. 

- `PDOStatement::bindParam()` method binds a parameter exclusively to a specified variable. The variable is bound as a reference.

The example code below shows how to execute a prepared statement that uses `PDOStatement::bindParam()` and `PDOStatement::bindValue()`:

```php
$data = array(
    'first_name' => 'Alisa',
    'birth_date' => '1999-06-30'
);

$pstmt = $conn->prepare("SELECT * FROM students WHERE first_name = ? AND birth_date = ?");
$pstmt->bindParam(1, $data['first_name'], PDO::PARAM_STR);
$pstmt->bindParam(2, $data['birth_date'], PDO::PARAM_STR);
$pstmt->execute();
```
- `$pstmt->bindParam(1, $data['first_name'], PDO::PARAM_STR);` and `$pstmt->bindParam(2, $data['birth_date'], PDO::PARAM_STR);` binds the array elements `$data['first_name]` and `$data['birth_date']` to the corresponding positional placeholders in the SQL statement which are `first_name = ?` and `birth_date = ?` respectively.

- `1`, `$data['first_name']`, `2`, `$data['birth_date']`, and `PDO::PARAM_STR` are arguments to be passed in the `bindParam()` method.

- `1` and `2` represent the index position as the parameter identifier.

- `$data['first_name']` and ` $data['birth_date']` represent the values to bind to the positional placeholders in the SQL statement.

- `PDO::PARAM_STR` is a predefined constant of a string data type or SQL CHAR, VARCHAR.

- `$pstmt->execute();` executes the prepared statement of `$pstmt`.

```php
$data = array(
    'first_name' => 'Alisa',
    'birth_date' => '1999-06-30'
);

$pstmt = $conn->prepare("SELECT * FROM students WHERE first_name = :first_name AND birth_date = :birth_date");
$pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);
$pstmt->bindValue(':birth_date', $data['birth_date'], PDO::PARAM_STR);

$pstmt->bindValue(':first_name', 'Alisa', PDO::PARAM_STR);
$pstmt->bindValue(':birth_date', '1999-06-30', PDO::PARAM_STR);
$pstmt->execute();
```
- `$pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);` and `$pstmt->bindValue(':birth_date', $data['birth_date'], PDO::PARAM_STR);` binds the array elements `$data[first_name]` and `$data[birth_date]` to the corresponding named placeholders `:first_name` and `:birth_date` in the SQL statement.

- `$pstmt->bindValue(':first_name', 'Alisa', PDO::PARAM_STR);` and `$pstmt->bindValue(':birth_date', '1999-06-30', PDO::PARAM_STR);` binds the values `Alisa` and `1999-06-30` to the corresponding named placeholders `:first_name` and `:birth_date` in the SQL statement.

- `:first_name`, `$data['first_name']`, `:birth_date`, `$data['birth_date']`, `Alisa`, `1999-06-30`, and `PDO::PARAM_STR` are arguments to be passed in the `bindValue()` method.

- `:first_name` and `:birth_date` represent the parameter identifiers.

- `$data['first_name']`, `$data['birth_date']`, `Alisa`, and `1999-06-30` represent the values to bind to the corresponding named placeholders in the SQL statement.