# Prepared Statement with Binding Methods

+++

### Part 1: Sample Code Analysis

:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = array(
        'min_birth_date' => '1999-01-01',
        'max_birth_date' => '2000-01-01'
    );
    
    $sql = "SELECT * FROM students WHERE birth_date >= :min_birth_date AND birth_date < :max_birth_date";

    $pstmt = $conn->prepare($sql);
    $pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);
    $pstmt->bindParam(':max_birth_date', $data['max_birth_date'], PDO::PARAM_STR);
    $pstmt->execute();
    $data = $pstmt->fetchAll();

    foreach ($data as $row) {
        echo $row['student_id'] . "\t";
        echo $row['first_name'] . " ";
        echo $row['last_name'] . "\t";
        echo $row['birth_date'] . "\t";
        echo $row['gender'] . "\n";
    }
?>
```
/// type=MS, answer=[1,2,3] 

Execute the program. What are printed on lines 2, 3, and 4?

- `1 John Smith 1999-02-10 M`

- `6 Alisa Ells 1999-06-30 F`

- `2 Samantha Danes 1999-10-12 F`

- `Unable to establish a connection.`

- `Successfully connected to the database.`


/// type=MS, answer=[2,3]

Which of the following are array values in the associative array `$data`?

- `students`

- `1999-01-01`

- `2000-01-01`

- `min_birth_date`

- `max_birth_date`


/// type=SS, answer=[4]

Which statement best describes the code on lines 5, 6, 7, and 8 of `Student.php`?

- It displays the elements of the associative array `$data`.

- It holds two keys with one value in each key such as `1999-01-01` and `2000-01-01`.

- It holds the elements of the associative array `$data` using the `array()` language construct.

- It creates the associative array named `$data` with two keys `min_birth_date` and `max_birth_date`.

- It accesses the elements of `$data` using the `array()` language construct and the short array syntax `[]`.


/// type=MS, answer=[4,5]

In `Student.php`, which of the following are named placeholders?

- `students`

- `birth_date`

- `min_birth_date`

- `:max_birth_date`

- `:min_birth_date`


/// type=SS, answer=[1]

In `Student.php`, what value is associated with the named placeholder `:min_birth_date` on line 10?

- `1999-01-01`

- `2000-01-01`

- `birth_date`

- `min_birth_date`

- `max_birth_date`


/// type=SS, answer=[2]

In `Student.php`, what value is associated with the named placeholder `:max_birth_date` on line 10?

- `1999-01-01`

- `2000-01-01`

- `birth_date`

- `min_birth_date`

- `max_birth_date`


/// type=SS, answer=[5]

Which statement best describes `WHERE birth_date >= :min_birth_date AND birth_date < :max_birth_date` on line 10 of `Student.php`?

- It selects the rows in the `students` table related to the values `1999-01-01` and `2000-01-01`.

- It selects the rows in the `students` table equivalent to the values `1999-01-01` and `2000-01-01`.

- It returns all records in the `students` table whose `birth_date` starts with `1999-01-01` or `2000-01-01`.

- It updates the rows in the `students` table whose `birth_date` is between the values `1999-01-01` and `2000-01-01`.

- It filters the rows in the `students` table whose `birth_date` is greater than or equal to the value `1999-01-01` and less than the value `2000-01-01`.


/// type=MS, answer=[2,3,4,5]

Which statements correctly describe `$pstmt = $conn->prepare($sql)` on line 12 of `Student.php`?

- It executes the SQL statement.

- It prepares the argument `$sql` for execution.

- It returns the result set as a `PDOStatement` object.

- It calls the `prepare()` method of the `$conn` object.

- It assigns the `PDOStatement` object to the variable `$pstmt`.


/// type=SS, answer=[3]

In `Student.php`, which of the following represents the parameter identifier in the statement `$pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);` on line 13?

- `$data`

- `PDO::PARAM_STR`

- `:min_birth_date`

- `$data['min_birth_date']`

- `(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR)`


/// type=SS, answer=[4]

In `Student.php`, which of the following represents the value to bind in the statement `$pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);` on line 13?

- `$data`

- `PDO::PARAM_STR`

- `:min_birth_date`

- `$data['min_birth_date']`

- `(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR)`


/// type=SS, answer=[3]

In `Student.php`, which argument represents the explicit data type in the statement `$pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);` on line 13?

- `$data`

- `min_birth_date`

- `PDO::PARAM_STR`

- `:min_birth_date`

- `$data['min_birth_date']`


/// type=MS, answer=[1,4]

In `Student.php`, which statements correctly describe `:min_birth_date`, `$data['min_birth_date']`, and `PDO::PARAM_STR` on line 13?

- These are arguments of the `bindParam()` method.

- They represent the key, array variable, data type of the parameter.

- They represent the variable, value, and data type of the parameter.

- They represent the parameter identifier, value, and data type of the parameter.

- They represent the key, array element, and constant data type of the parameter.


/// type=SS, answer=[4]

In `Student.php`, what does the `bindParam()` method do on line 13?

- It assigns the value `1999-01-01` to the named placeholder `:min_birth_date`.

- It updates the value `1990-01-01` to the named placeholder as parameter `:min_birth_date`.

- It modifies the value `2000-01-01` to the named placeholder as parameter `:max_birth_date`.

- It binds the value of `$data['min_birth_date']` to the corresponding named placeholder `:min_birth_date`.

- It binds the value of `$data['max_birth_date']` to the corresponding named placeholder `:max_birth_date`.


/// type=MS, answer=[2,3,5]

Which statements correctly describe `$pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);` on line 13?

- It executes the SQL statement.

- It returns the boolean value `true`.

- It calls the `bindParam()` method of the `$pstmt` object.

- It assigns the named placeholder `:min_birth_date` to `$pstmt`.

- It binds the value of `$data['min_birth_date]` to the named placeholder `:min_birth_date` in the SQL statement.


/// type=SS, answer=[4]

In `Student.php`, which of the following represents the value to bind in the statement `$pstmt->bindParam(':max_birth_date', $data['max_birth_date'], PDO::PARAM_STR);` on line 14?

- `$data`

- `max_birth_date`

- `:max_birth_date`

- `$data['max_birth_date']`

- `(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR)`


/// type=SS, answer=[4]

In `Student.php`, which of the following represents the parameter identifier in the statement `$pstmt->bindParam(':max_birth_date', $data['max_birth_date'], PDO::PARAM_STR);` on line 14?

- `$data`

- `PDO::PARAM_STR`

- `max_birth_date`

- `:max_birth_date`

- `$data['max_birth_date']`


/// type=SS, answer=[5]

In `Student.php`, what does the `bindParam()` method do on line 14?

- It assigns the value `2000-01-01` to the named placeholder `:max_birth_date`.

- It modifies the named placeholder `:max_birth_date` to the value `2000-01-01`.

- It binds the value of `$data['min_birth_date']` to the corresponding named placeholder `:min_birth_date`.

- It updates the named placeholder `:max_birth_date` to the specified array element `$data[max_birth_date]`.

- It binds the value of `$data['max_birth_date']` to the corresponding named placeholder `:max_birth_date`.


/// type=SS, answer=[3]

In `Student.php`, what does the `execute()` method do on line 15?

- It executes the SQL statement.

- It executes the argument `$pstmt`.

- It executes the prepared statement `$pstmt`.

- It fetches the result set of the `bindParam()` method.

- It duplicates the named placeholders in the `bindParam()` method.


/// type=MS, answer=[2,3,5]

Which statements correctly describe the code on line 16 of `Student.php`?

- It queries the SQL statement.

- It calls the `fetchAll()` method of the `$pstmt` object.

- It returns the array containing all of the result set rows.

- It executes the argument `$pstmt` in the `fetchAll()` method.

- It assigns the returned value of `fetchAll()` method to the variable `$data`.

:::


:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD); 
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $sql = "DELETE FROM students WHERE first_name = ? AND last_name = ?";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindValue(1, 'John');
        $pstmt->bindValue(2, 'Smith');
        if (!$pstmt->execute()) {
            throw new Exception("Unable to delete student data in the table.");
        }
        echo "Successfully deleted the student data in the table.";
    } catch (Execption $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `Unable to delete student data in the table.`.

- It prints `Successfully connected to the database.` and `Successfully deleted the student data in the table.`.


/// type=SS, answer=[1]

Which variable holds the SQL statement in `Student.php`?

- `$sql`

- `$conn`

- `$pstmt`

- `last_name`

- `first_name`


/// type=SS, answer=[1]

In `Student.php`, which of the following is a positional placeholder?

- `?`

- `$sql`

- `students`

- `DELETE FROM`

- `first_name = ?`


/// type=SS, answer=[4]

In the statement `$pstmt->bindValue(1, 'John');` on line 9 of `Student.php`, what is `1`?

- It represents the named placeholder.

- It represents the explicit data type for the parameter.

- It represents the value to bind to the positional placeholder `?` in the SQL statement. 

- It represents the 1-index position of the positional placeholder `?` in the SQL statement.

- It represents the variable to bind to the positional placeholder `?` in the SQL statement. 


/// type=SS, answer=[4]

In the statement `$pstmt->bindValue(1, 'John');` on line 9 of `Student.php`, what does `John` represent?

- The explicit data type.

- The named placeholder.

- The 1-index position of the parameter.

- The value to bind to the positional placeholder `?`.

- The variable to bind to the positional placeholder `?`.


/// type=MS, answer=[1,4]

Which statements correctly describe `1` and `John` on line 9 of `Student.php`?

- These are the arguments of the `bindValue()` method.

- They represent the key and array value of the parameter.

- They represent the key and array element of the parameter.

- They represent the 1-index position and value of the parameter.

- They represent the variable and constant data type of the parameter.


/// type=SS, answer=[2]

In `Student.php`, what does `bindValue()` do on line 9?

- It binds the value `John` to the corresponding positional placeholder `?` in `last_name = ?` of the SQL statement.

- It binds the value `John` to the corresponding positional placeholder `?` in `first_name = ?` of the SQL statement.

- It assigns the value `John` to the corresponding positional placeholder `?` in `last_name = ?` of the SQL statement.

- It replaces the value `John` to the corresponding positional placeholder `?` in `last_name = ?` of the SQL statement.

- It replaces the value `John` to the corresponding positional placeholder `?` in `first_name = ?` of the SQL statement.


/// type=MS, answer=[2,4,5]

Which statements correctly descibe `$pstmt->bindValue(1, 'John');` on line 9 of `Student.php`?

- It executes the SQL statement.

- It returns the boolean value `true`.

- It assigns the value `John` to `$pstmt`.

- It calls the `bindValue()` method of the `$pstmt` object.

- It binds the value `John` to the corresponding positional placeholder `?` in `first_name = ?` of the SQL statement.


/// type=SS, answer=[1]

In `Student.php`, which of the following represents the 1-index position as the parameter identifier on line 10?

- `2`

- `->`

- `Smith`

- `$pstmt`

- `bindValue()`


/// type=SS, answer=[1]

In `Student.php`, what does `bindValue()` do on line 10?

- It binds the value `Smith` to the corresponding positional placeholder `?` in `last_name = ?` of the SQL statement.

- It binds the value `John` to the corresponding positional placeholder `?` in `first_name = ?` of the SQL statement.

- It assigns the value `Smith` to the corresponding positional placeholder `?` in `last_name = ?` of the SQL statement.

- It replaces the value `John` to the corresponding positional placeholder `?` in `first_name = ?` of the SQL statement.

- It replaces the value `Smith` to the corresponding positional placeholder `?` in `last_name = ?` of the SQL statement.

:::


:::

/// type=REPL, init=[commands/BindingMethods/DeleteJohnSmithStudentData.sql], filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");
    
    $conn = Connection::getConnection();
    $data = array(
        'first_name' => 'John',
        'last_name' => 'Smith'
    );

    $sql = "SELECT * FROM students WHERE first_name = :first_name and last_name = :last_name";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);
        $pstmt->bindValue(':last_name', $data['last_name'], PDO::PARAM_STR);
        $pstmt->execute();
        $data = $pstmt->fetchAll();
        if (empty($data)) {
            throw new Exception("Student record not found.");
        }
        foreach ($data as $row) {
            echo $row['student_id'] . "\t";
            echo $row['first_name'] . " ";
            echo $row['last_name'] . "\t";
            echo $row['birth_date'] . "\t";
            echo $row['gender'] . "\n";
        }
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.`.

- It prints `Successfully connected to the database.` and `Student record not found.` in separate lines.


/// type=SS, answer=[5]

On lines 6 and 7 of `Student.php`, replace the strings `John` and `Smith` with `Alisa` and `Ells`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `Student record not found.` in separate lines.

- It prints `Successfully connected to the database.` and `6 Alisa Ells 1999-06-30 F` in separate lines.

:::


:::

/// type=REPL, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = array(
        'first_name' => 'Alisa',
        'last_name' => 'Ells'
    );
    
    $sql = "SELECT * FROM students WHERE first_name = :first_name and last_name = :last_name";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindValue(':first_name', $data['first_name'], PDO::PARAM_STR);
        $pstmt->bindValue(':last_name', $data['last_name'], PDO::PARAM_STR);
        $pstmt->execute();
        $data = $pstmt->fetchAll();
        if (empty($data)) {
            throw new Exception("Student record not found.");
        }
        foreach ($data as $row) {
            echo $row['student_id'] . "\t";
            echo $row['first_name'] . " ";
            echo $row['last_name'] . "\t";
            echo $row['birth_date'] . "\t";
            echi $row['gender'] . "\n";
        }
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[5]

On lines 14 and 15 of `Student.php`, replace the `bindValue()` method with `bindParam()`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `Student record not found.` in separate lines.

- It prints `Successfully connected to the database.` and `6 Alisa Ells 1999-06-30 F` in separate lines.

:::


:::

/// type=REPL, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = array(
        'first_name' => 'Alisa',
        'last_name' => 'Ells'
    );
    
    $sql = "SELECT * FROM students WHERE first_name = :first_name and last_name = :last_name";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindParam(':first_name', $data['first_name'], PDO::PARAM_STR);
        $pstmt->bindParam(':last_name', $data['last_name'], PDO::PARAM_STR);
        $pstmt->execute();
        $data = $pstmt->fetchAll();
        if (empty($data)) {
            throw new Exception("Student record not found.");
        }
        foreach ($data as $row) {
            echo $row['student_id'] . "\t";
            echo $row['first_name'] . " ";
            echo $row['last_name'] . "\t";
            echo $row['birth_date'] . "\t";
            echi $row['gender'] . "\n";
        }
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=MS, answer=[3,5]

Which statements correctly describe the code on lines 18, 19, and 20 of `Student.php`?

- It adds the values to `$data`.

- It displays the values of `$data`.

- It returns the boolean value `false`.

- It assigns the values to the array variable `$data`.

- It checks the array variable `$data` if empty or not.

:::


:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = ['Naomi', 'Wolf'];
    $sql = "CREATE TABLE IF NOT EXISTS authors (PRIMARY KEY (author_id), author_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80))";
            
   try {
        $stmt = $conn->query($sql);
        if (!$stmt) {
           throw new Exception("Unable to create a table.");
        }
        $pstmt = $conn->prepare("INSERT INTO authors (first_name, last_name) VALUES (?,?)");
        $pstmt->bindParam(1, $data[0], PDO::PARAM_STR);
        $pstmt->bindParam(2, $data[1], PDO::PARAM_STR);
        if (!$pstmt->execute()) {
             throw new Exception("Unable to insert values into the table.");
        }
       echo "Successfully created the table and inserted values into the table.";
   } catch (Exception $e) {
       echo $e->getMessage();
   }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `Unable to create a table.`.

- It prints `Successfully connected to the database.` and `Unable to insert values into the table.`.

- It prints `Successfully connected to the database.` and `Successfully created the table and inserted values into the table.`.


/// type=MS, answer=[3,4]

What are the SQL statements used in `Student.php`?

- `VALUES`

- `UPDATE`

- `INSERT INTO`

- `CREATE TABLE`

- `INT GENERATED AS ALWAYS`


/// type=SS, answer=[1]

In `Student.php`, which variable holds the statement `CREATE TABLE IF NOT EXISTS authors (PRIMARY KEY (author_id), author_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80))`?

- `$sql`

- `$data`

- `$stmt`

- `$conn`

- `$pstmt`


/// type=MS, answer=[4,5]

In `Student.php`, what does the `query()` method do on line 9?

- It holds the value of `$sql`.

- It returns the boolean value `true`.

- It executes the prepared statement.

- It returns the result set as a `PDOStatement` object.

- It executes the SQL statement in a single function call.


/// type=MS, answer=[3,4]

Which statements correctly describe the code on lines 10, 11, and 12 of `Student.php`?

- The `if` statement evaluates to `true` and the statement on line 10 is executed.

- The `if` statement executes the returned value `$stmt` inside the parentheses `()`.

- The `if` statement evaluates the negated value of `$stmt` inside the parentheses `()`.

- The `if` statement evaluates to `false` and the statement on line 10 is not executed.

- The `if` statement evaluates to `true` and it displays the string `Unable to create a table.`.


/// type=SS, answer=[1]

In `Student.php`, which of the following is a positional placeholder?

- `?`

- `$data`

- `$pstmt`

- `['Naomi', 'Wolf']`

- `(first_name, last_name)`


/// type=SS, answer=[3]

What value is assigned to `$data[0]` on line 14?

- `?`

- `Wolf`

- `Naomi`

- `last_name`

- `first_name`


/// type=MS, answer=[3,4]

In `Student.php`, which arguments represent the values that are passed to the positional placeholders `?` on line 13?

- `1`

- `2`

- `$data[0]`

- `$data[1]`

- `PDO::PARAM_STR`


/// type=SS, answer=[2]

What value is assigned to `$data[1]` on line 15?

- `?`

- `Wolf`

- `Naomi`

- `last_name`

- `first_name`


/// type=SS, answer=[2]

In `Student.php`, which argument represents the 1-index position of the positional placeholder `?` on line 15?

- `1`

- `2`

- `$data[0]`

- `$data[1]`

- `PDO::PARAM_STR`

:::


:::

/// type=REPL, init=[commands/BindingMethods/CreateAuthorsTableAndInsertData.sql], filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $author_name = 'Naomi';
    $sql = "SELECT * FROM authors WHERE first_name = :first_name";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindValue(':first_name', $author_name, PDO::PARAM_STR);
        $pstmt->execute();
        $data = $pstmt->fetchAll();
        if (empty($data)) {
            throw new Exception("Student record not found.");
        }
        foreach ($data as $row) {
            echo $row['author_id'] . "\t";
            echo $row['first_name'] . "\t";
            echo $row['last_name'] . "\n";
        }
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[4]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `1 Naomi Wolf` in separate lines.

- It prints `Successfully connected to the database.` and `Student record not found.` in separate lines.


/// type=SS, answer=[4]

In the statement `$pstmt->bindValue(':first_name', $author_name, PDO::PARAM_STR);` on line 10 of `Student.php`, replace the variable `$author_name` with the value `Naomi`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `1 Naomi Wolf` in separate lines.

- It prints `Successfully connected to the database.` and `Student record not found.` in separate lines.

:::


+++


+++

### Part 2: Knowledge Assessment

/// type=SS, answer=[1]

Which statement best describes `PDOStatement::bindValue()`?

- It binds a value to a parameter

- It executes a prepared statement.

- It binds a parameter to a variable.

- It sets a proper data type in an SQL statement.

- It sets a value to bind to the corresponding placeholder as a parameter.


/// type=MS, answer=[2,3,4]

Which statements correctly describe `PDOStatement::bindParam()`?

- It executes a prepared statement.

- It binds a parameter to a variable.

- It sets a bounded variable as a reference.

- It evaluates a bounded variable when the `execute()` method is called.

- It sets the values to bind to the corresponding placeholder as a parameter. 


/// type=MS, answer=[1,3,5]

What arguments are passed in `PDOStatement::bindValue()`?

- A parameter identifier.

- A row number of the parameter.

- A value to bind to the parameter.

- A return value either `true` or `false`. 

- An explicit data type for the parameter.


/// type=MS, answer=[1,4,5]

What arguments are passed in `PDOStatement::bindParam()`?

- A parameter identifier.

- A row number of the parameter.

- A value to bind to the parameter.

- A parameter to bind to the variable.

- An explicit data type for the parameter.


/// type=SS, answer=[5]

Which statement best describes `PDO::PARAM_STR`?

- It is a predefined constant that represents a boolean data type.

- It is a predefined constant that represents an `SQL NULL` data type

- It is a predefined constant that represents an `SQL INTEGER` data type.

- It is a predefined constant that represents an SQL large object data type.

- It is a predefined constant that represents an `SQL CHAR`, `VARCHAR`, or other string data type.

+++


+++

### Part 3: Finding and Fixing Errors

:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = array(
        'min_birth_date' => '1999-01-01',
        'max_birth_date' => '2000-01-01'
    );
    
    $sql = "SELECT * FROM students WHERE birth_date >= ? AND birth_date < ?";

    $pstmt = $conn->prepare($sql);
    $pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);
    $pstmt->bindParam('2', $data['max_birth_date'], PDO::PARAM_STR);
    $pstmt->execute();

    $data = $pstmt->fetchAll();

    foreach ($data as $row) {
        echo $row['student_id'] . "\t";
        echo $row['first_name'] . " ";
        echo $row['last_name'] . "\t";
        echo $row['birth_date'] . "\t";
        echo $row['gender'] . "\n";
    }
?>
```
/// type=SS, answer=[2]

Execute the program. What is the error message?

- syntax error, unexpected `$pstmt` on line 12

- Invalid parameter number: `:min_birth_date` on line 13

- Invalid parameter number: `:max_birth_date` on line 14

- `PDO::prepare()` expects at least 1 parameter, 0 given on line 12

- syntax error, unexpected `$data` (T_VARIABLE), expecting `,` or `)` on line 13 


/// type=MS, answer=[3,5]

Which statements correctly describe the error?

- The named placeholder `:min_birth_date` is enclosed in single quotes `''` on line 13.

- In `Student.php`, the semicolon `;` and close parenthesis `)` are misplaced on line 8.

- On line 13, the parameter identifier `:min_birth_date` should be an index position of value `1`.

- On lines 6 and 7, the values set by the keys `min_birth_date` and `max_birth_date` is incorrect.

- On line 13, the parameter identifier `:min_birth_date` in the statement `$pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);` is incorrect.

:::


/// type=CR, answer=[tests/BindingMethods/IncorrectParameterIdentifierInBindParamArgument.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs `Successfully connected to the database.`, `2 Samantha Danes 1999-10-12 F`, and `6 Alisa Ells 1999-06-30 F` in separate lines.

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);

            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = array(
        'min_birth_date' => '1999-01-01',
        'max_birth_date' => '2000-01-01'
    );
    
    $sql = "SELECT * FROM students WHERE birth_date >= ? AND birth_date < ?";

    $pstmt = $conn->prepare($sql);
    $pstmt->bindParam(':min_birth_date', $data['min_birth_date'], PDO::PARAM_STR);
    $pstmt->bindParam('2', $data['max_birth_date'], PDO::PARAM_STR);
    $pstmt->execute();

    $data = $pstmt->fetchAll();

    foreach ($data as $row) {
        echo $row['student_id'] . "\t";
        echo $row['first_name'] . " ";
        echo $row['last_name'] . "\t";
        echo $row['birth_date'] . "\t";
        echo $row['gender'] . "\n";
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $sql = "DELETE FROM students WHERE first_name = ? AND last_name = ?";

    try {
        $pstmt = $conn->prepare($sql);
        bindValue(1, 'John');
        bindValue(2, 'Smith');
        if (!$pstmt->execute()) {
            throw new Exception("Unable to delete student data in the table.");
        }
        echo "Successfully deleted the student data in the table.";
    } catch (Execption $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is the error message?

- syntax error, unexpected `}` on line 12 

- syntax error, unexpected `try` on line 7

- syntax error, unexpected `$sql` on line 5

- syntax error, unexpected `bindValue` on line 9

- Call to undefined function `bindValue()` thrown on line 9


/// type=MS, answer=[4,5]

Which statements correctly describe the error?

- On line 8, the argument passed is `$sql`.

- On line 5, the SQL statement is enclosed in double quotes `""`.

- On lines 9 and 10, the index positions `1` and `2` of the parameter are not enclosed in single quotes `''`.

- On lines 9 and 10, the statements `bindValue(1, 'John')` and `bindValue(2, 'Smith');` are incorrect.

- In `Student.php`, there are no `$pstmt` object and object operator `->` before the `bindValue()` method on lines 9 and 10. 

:::


/// type=CR, answer=[tests/BindingMethods/MissingObjectAndOperatorInBindValue.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully deleted the student data in the table.`.

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $sql = "DELETE FROM students WHERE first_name = ? AND last_name = ?";

    try {
        $pstmt = $conn->prepare($sql);
        bindValue(1, 'John');
        bindValue(2, 'Smith');
        if (!$pstmt->execute()) {
            throw new Exception("Unable to delete student data in the table.");
        }
        echo "Successfully deleted the student data in the table.";
    } catch (Execption $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = ['Carlo','Pears'];

    $sql = "SELECT * FROM students WHERE first_name = ? and last_name = ?";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindValue(1, $data[0], PDO::PARAM_STR);
        $pstmt->bindValue(2, $data[1], PDO::PARAM_STR);
        $pstmt->execute();
        $data = fetchAll();
        if (empty($data)) {
            throw new Exception("Student record not found.");
        }
        foreach ($data as $row) {
            echo $row['student_id'] . "\t";
            echo $row['first_name'] . " ";
            echo $row['last_name'] . "\t";
            echo $row['birth_date'] . "\t";
            echo $row['gender'] . "\n";
        }
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[3]

Execute the program. What is its output?

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and produces an error.

- It prints `Successfully connected to the database.` and `Student record not found` in separate lines.

- It prints `Successfully connected to the database.` and `7 Carlo Pears 1998-04-04 M` in separate lines.


/// type=SS, answer=[4]

What is the error message?

- Undefined variable: `conn` on line 10

- syntax error, unexpected `,` on line 5

- syntax error, unexpected `$pstmt` on line 13

- Call to undefined function `fetchAll()` on line 14

- Call to a member function `prepare()` on null on line 10


/// type=MS, answer=[1,5]

Which statements correctly describe the error?

- On lines 14, the statement `$data = fetchAll();` is incorrect.

- There are no parentheses `()` that enclosed the SQL statement on line 7.

- On line 5, the values `Carlo` and `Pears` are enclosed in single quotes `""`.

- On line 5, there is no `array()` language construct to create and initialize the array variable `$data`.

- In `Student.php`, there are no `$pstmt` object and object operator `->` before the `fetchAll()` method on line 14.

:::


/// type=CR, answer=[tests/BindingMethods/MissingObjectAndOperatorInFetchAll.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `7 Carlo Pears 1998-04-04 M` in separate lines.

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    $conn = Connection::getConnection();
    $data = ['Carlo','Pears'];

    $sql = "SELECT * FROM students WHERE first_name = ? and last_name = ?";

    try {
        $pstmt = $conn->prepare($sql);
        $pstmt->bindValue(1, $data[0], PDO::PARAM_STR);
        $pstmt->bindValue(2, $data[1], PDO::PARAM_STR);
        $pstmt->execute();
        $data = fetchAll();
        if (empty($data)) {
            throw new Exception("Student record not found.");
        }
        foreach ($data as $row) {
            echo $row['student_id'] . "\t";
            echo $row['first_name'] . " ";
            echo $row['last_name'] . "\t";
            echo $row['birth_date'] . "\t";
            echo $row['gender'] . "\n";
        }
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[Connection.php,Student.php]

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");
    
    $conn = Connection::getConnection();
    $data = 'Anne','Frank';

    try {
        $pstmt = $conn->prepare("INSERT INTO authors (first_name, last_name) VALUES (?, ?)");
        $pstmt->bindParam(1, $data[0], PDO::PARAM_STR);
        $pstmt->bindParam(2, $data[1], PDO::PARAM_STR);
        if (!$pstmt->execute()) {
            throw new Exception("Unable to insert values into the table.");
        }
         echo "Successfully inserted values into the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[1]

Execute the program. What is the error message?

- syntax error, unexpected `,` on line 5

- Unable to insert values into the table.

- syntax error, unexpected `$pstmt` on line 9

- Call to undefined function `bindParam()` on line 9

- syntax error, unexpected `INTO` (T_STRING), expecting `,` on line 8


/// type=MS, answer=[1,4]

Which statements correctly describe the error?

- On line 5, the statement `$data = 'Anne','Frank;'` is incorrect.

- On line 5, the strings `Anne` and `Frank` are enclosed in single quotes `''`.

- On line 5, a comma `,` between the values `Anne` and `Frank` is not allowed.

- On line 5, the strings `Anne` and `Frank` are not enclosed in square brackets `[]`.

- There are no parentheses `()` that enclosed the values `Anne` and `Frank` on line 5.

:::

/// type=CR, answer=[tests/BindingMethods/MissingSquareBrackets.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully inserted values into the table.`.

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");
    
    $conn = Connection::getConnection();
    $data = 'Anne','Frank';

    try {
        $pstmt = $conn->prepare("INSERT INTO authors (first_name, last_name) VALUES (?,?)");
        $pstmt->bindParam(1, $data[0], PDO::PARAM_STR);
        $pstmt->bindParam(2, $data[1], PDO::PARAM_STR);
        if (!$pstmt->execute()) {
            throw new Exception("Unable to insert values into the table.");
        }
        echo "Successfully inserted values into the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```

+++


+++

### Part 4: Practice

/// type=CR, answer=[tests/BindingMethods/CreatePHPProgramUsingBindValue.php], init=[commands/BindingMethods/InsertAnneFrankValue.sql], filename=[Connection.php,Author.php]

Write a PHP program named `Author.php` that includes the `Connection.php` file to insert an author data into the `authors` table and use the `bindValue()` method to bind a value to a parameter. In `Author.php` tab, add the `require_once()` statement to have the `Connection.php` file included. Then, add the `try` and `catch` statements. Inside the `try` block, add a statement that assigns the `prepare()` method call of the `$conn` object which passes the argument `INSERT INTO authors (first_name, last_name) VALUES (?, ?)` to the `$pstmt` variable. Then, add the `bindValue()` method call of the `$pstmt` object which contains the arguments `1`, `Stephen`, and `PDO::PARAM_STR`. Add another `bindValue()` method call of the `$pstmt` object which contains the arguments `2`, `Hawking`, and `PDO::PARAM_STR`. Next, add the `if` statement that evaluates the negated statement `$pstmt->execute()` inside the parentheses `()`. Inside the `if` block, add a statement that throws an exception message `Unable to insert values into the table.`. After the `if` block, add the `echo` statement that displays the string `Successfully inserted values into the table.`. Then, inside the `catch` block, add the statement `echo $e->getMessage();`. Run the program to view the output. 

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php



?>
```

/// type=CR, answer=[tests/BindingMethods/CreatePHPProgramUsingBindParam.php], init=[commands/BindingMethods/InsertStephenHawkingData.sql], filename=[Connection.php,Author.php]

Write a PHP program named `Author.php` that includes the `Connection.php` file to insert an author data into the `authors` table and use the `bindParam()` method to bind a parameter to a specific variable. In `Author.php` tab, add the `require_once()` statement to have the `Connection.php` file included. Create an array variable named `$data` and assign the elements `['Farley', 'Mowat']` using the `array()` language construct. Then, add the `try` and `catch` statements. Inside the `try` block, add a statement that assigns the `prepare()` method call of the `$conn` object which passes the argument `INSERT INTO authors (first_name, last_name) VALUES (:first_name, :last_name)` to the `$pstmt` variable. Then, add the `bindParam()` method call of the `$pstmt` object which contains the arguments `:first_name`, `$data[0]`, and `PDO::PARAM_STR`. Add another `bindParam()` method call of the `$pstmt` object which contains the arguments `:last_name`, `$data[1]`, and `PDO::PARAM_STR`. Next, add the `if` statement that evaluates the negated statement `$pstmt->execute()` inside the parentheses `()`. Inside the `if` block, add a statement that throws an exception message `Unable to insert values into the table.`. After the `if` block, add the `echo` statement that displays the string `Successfully inserted values into the table.`. Then, inside the `catch` block, add the statement `echo $e->getMessage();`. Run the program to view the output. 

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection()
        {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
            } catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php



?>
```

+++