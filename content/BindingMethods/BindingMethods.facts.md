### Facts for Prepared Statement with Binding Methods

Parameter binding is useful to set the proper data type explicitly. The `bindValue()` and `bindParam()` methods bind values or variables in a prepared statement that contains positional `?` or named `:variable_name` placeholders as parameters.

- The `PDOStatement::bindValue()` method binds a value to a parameter.

- The `PDOStatement::bindParam()` method binds a parameter to a variable. The variable is bound as a reference and will be evaluated when the `PDOStatement::execute()` is called.

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
- `$pstmt->bindParam(1, $data['first_name'], PDO::PARAM_STR);` and `$pstmt->bindParam(2, $data['birth_date'], PDO::PARAM_STR);` binds `$data['first_name]` and `$data['birth_date']` to the corresponding positional placeholders `?` in `first_name = ?` and `birth_date = ?` of the SQL statement.

- `1`, `$data['first_name']`, `2`, `$data['birth_date']`, and `PDO::PARAM_STR` are arguments in the `bindParam()` method.

- `1` and `2` represent the 1-index position of the positional placeholders `?` as parameters.

- `$data['first_name']` and `$data['birth_date']` represent the values to bind to the positional placeholders `?` in the SQL statement.

- `PDO::PARAM_STR` represents a predefined constant `SQL CHAR`, `VARCHAR`, or other string data type for the parameter. A few other types of predefined constants are:
    - `PDO::PARAM_BOOL` for a boolean data type.
    - `PDO::PARAM_NULL` for SQL null data type. 
    - `PDO::PARAM_INT` for SQL integer data type.

- `$pstmt->execute();` executes the prepared statement `$pstmt`.

```php
$data = array(
    'first_name' => 'Alisa'
);

$pstmt = $conn->prepare("SELECT * FROM students WHERE first_name = :first_name AND birth_date = :birth_date");
$pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);
$pstmt->bindValue(':birth_date', '1999-06-30', PDO::PARAM_STR);
$pstmt->execute();
```
- `$pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);` and `$pstmt->bindValue(':birth_date', '1999-06-30', PDO::PARAM_STR);` binds `$data[first_name]` and `1999-06-30` to the corresponding named placeholders `:first_name` and `:birth_date` in the SQL statement.

- `:first_name`, `$data['first_name']`, `:birth_date`, `1999-06-30`, and `PDO::PARAM_STR` are arguments in the `bindValue()` method.

- `:first_name` and `:birth_date` represent the parameter identifier for the named placeholders in the SQL statement.

- `$data['first_name']` and `1999-06-30` represent the values to bind to the corresponding named placeholders `:first_name` and `:birth_date` in the SQL statement.