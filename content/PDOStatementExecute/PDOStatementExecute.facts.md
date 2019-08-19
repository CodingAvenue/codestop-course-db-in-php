### Facts for Prepared Statement with Execute

`PDOStatement::execute()` executes a prepared statement. If it includes placeholders as parameters such as a positional placeholder `?` or named placeholder `:variable_name` you may either use `bindParam()` or `bindValue()` to bind either variables or values to the parameters.

`PDOStatement::bindValue` binds a value to a parameter. It passes both a `value` and `variable`.

`PDOStatement::bindParam` binds a parameter to a specified variable name. It can pass only a `variable`.

The example code below shows how to execute a prepared statement using `PDOStatement::bindParam()` and `PDOStatement::bindValue()`:

```php
// bindParam() can only pass a variable
$data = array(
    'first_name' => 'Alisa',
    'birth_date' => '1999-06-30'
);

$pstmt = $conn->prepare("SELECT * FROM students WHERE first_name = ? AND birth_date = ?");
$pstmt->bindParam(1, $data['first_name'], PDO::PARAM_STR);
$pstmt->bindParam(2, $data['birth_date'], PDO::PARAM_STR);
$pstmt->execute();

```

- `pstmt->bindParam(1, $data['first_name'], PDO::PARAM_STR);` binds the positional placeholder `first_name = ?` in the SQL statement passing the argument `(1, $data['first_name'], PDO::PARAM_STR)`.

- `$pstmt->bindParam(2, $data['birth_date'], PDO::PARAM_STR);` binds the positional placeholder `birth_date = ?` in the SQL statement passing the argument `(2, $data['birth_date'], PDO::PARAM_STR)`.

- The `(1, $data['first_name'], PDO::PARAM_STR)` and `(2, $data['birth_date'], PDO::PARAM_STR)` arguments contain the index position of the parameter, variable to bind to the placeholder, and explicit data type for the parameter.

- The `PDO::PARAM_STR` is a predefined constant that represents a string data type.

- `$pstmt->execute();` executes the prepared statement.

```php
// bindValue() passing a value
$pstmt = $conn->prepare("SELECT * FROM students WHERE first_name = :first_name AND birth_date = :birth_date");
$pstmt->bindValue(':first_name', 'Alisa', PDO::PARAM_STR);
$pstmt->bindValue(':birth_date', '1999-06-30', PDO::PARAM_STR);
$pstmt->execute();

```
- `$pstmt->bindValue(':first_name', 'Alisa', PDO::PARAM_STR);` binds the named parameter `:first_name` in the SQL statement passing the argument `(':first_name', 'Alisa', PDO::PARAM_STR)`.

- `$pstmt->bindValue(':birth_date', '1999-06-30', PDO::PARAM_STR);` binds the named parameter `:birth_date` in the SQL statement passing the argument `(':birth_date', '1999-06-30', PDO::PARAM_STR)`.

- The `(':first_name', 'Alisa', PDO::PARAM_STR)` and `(':birth_date', '1999-06-30', PDO::PARAM_STR)` arguments hold the named placeholder as the paramter identifier, value, and explicit data type for the parameter.

```php
// bindValue() passing an array variable
$data = array(
    'first_name' => 'Alisa',
    'birth_date' => '1999-06-30'
);

$pstmt = $conn->prepare("SELECT * FROM students WHERE first_name = :first_name AND birth_date = :birth_date");
$pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);
$pstmt->bindValue(':birth_date', $data['birth_date'], PDO::PARAM_STR);
$pstmt->execute();

```
- `$pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);` binds the named parameter `:first_name` in the SQL statement passing the arugment `(':first_name', $data['first_name'], PDO::PARAM_STR)`.

- The `(':first_name', $data['first_name'], PDO::PARAM_STR)` and `(':birth_date', $data['birth_date'], PDO::PARAM_STR)` arguments contain the named placeholder as the parameter identifier, variable, and explicit data type for the parameter.