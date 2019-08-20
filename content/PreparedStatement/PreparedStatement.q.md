# Prepared Statement

+++

### Part 1: Sample Code Analysis

:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/PreparedStatement/InsertValuesBerryVikkiIntoStudentTable.sql]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
        'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
    );
     
    try {
        $pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)");
        foreach ($data as $row) {
            if (!$pstmt->execute($row)) {
                throw new Exception("Unable to insert values into the table.");
            }
        }
        echo "Successfully inserted values into the table.";
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

- It prints `Successfully connected to the database.` and `Unable to insert values into the table.`.

- It prints `Successfully connected to the database.` and `Successfully inserted values into the table.`.


/// type=MS, answer=[4,5]

Which statements correctly describe the code on line 9 of `connection.php`?

- It evaluates the `$conn` object.

- It sets the `PDO` class to the `PDO_PGQSL DSN` statement

- It assigns the `PDO_PGQSL DSN` statement to the `PDO` class.

- It creates the `$conn` object as an instance of the `PDO` class.

- It passes the `PDO_PGQSL DSN` statement as an argument of the `PDO` class.


/// type=SS, answer=[3]

In `student.php`, what does the statement `require_once("connection.php");` do on line 2?

- It updates the file `connection.php`.

- It establishes a connection to the PostgreSQL database.

- It includes the file `connection.php` in the file `student.php`.

- It removes the file `connection.php` in the file `student.php`.

- It excludes the file `connection.php` in the file `student.php`.


/// type=MS, answer=[1,2,3,4,5]

Which of the following are array values in the multidimensional array `$data`?

- `Male`

- `Berry`

- `Vikki`

- `Meisner`

- `2002-09-09`


/// type=MS, answer=[2,4]

Which statements correctly describe the code on lines 4, 5, 6, and 7 of `student.php`?

- It displays the elements of the multidimensional array `$data`.

- It contains two keys `student1` and `student2` with four values in each key. 

- It removes the elements of the multidimensional array `$data` using the `array()` construct.

- It creates the multidimensional array named `$data` with two keys `student1` and `student2`.

- It accesses the elements of `$data` using the `array()` construct and the `[]` short array syntax.


/// type=MS, answer=[2,3]

In `student.php` what does the `prepare()` method do on line 10?

- It executes the SQL statement.

- It returns the `PDOStatement` object.

- It prepares the SQL statement for execution.

- It contains the result set of the remaining rows.

- It substitutes the input values of the SQL statement.


/// type=SS, answer=[3]

In `student.php`, what value is returned by `$conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)")` on line 10?

- The SQL statement.

- The DSN parameters.

- The `PDOStatment` object.

- The values of the variable array `$data`.

- The elements of the variable array `$data`.


/// type=SS, answer=[3]

In `student.php`, what does `$pstmt` do on line 10?

- It stores the SQL statement.

- It executes the SQL statement.

- It holds the `PDOStatement` object.

- It inserts values into the `students` table.

- It stores the values of the `students` table.


/// type=SS, answer=[3]

In `student.php`, which of the following represents the positional placeholder as a parameter?

- `students`

- `(?,?,?,?)`

- `first_name`

- `INSERT INTO`

- `(first_name, last_name, birth_date, gender)`


/// type=SS, answer=[5]

In `student.php`, what does the positional placeholders as parameters `(?,?,?,?)` do on line 10?

- It removes question mark values in the SQL statement.

- It inserts question marks as values to the `students` table.

- It sets random values of question marks to the SQL statement.

- It replaces the values in the SQL statement with question marks to have random values.

- It substitutes the values in the SQL statement with question marks to prevent SQL injection attacks.


/// type=MS, answer=[1,5]

In `student.php`, which statements correctly describe `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)` on line 10?

- It sets to add new records into the `students` table.

- It replaces the values in the SQL statement with question marks `?,?,?,?`.

- It uses question marks `?,?,?,?` as parameters to be inserted into the `students` table.

- It modifies the values to be inserted into the `students` table with positional placeholders `?,?,?,?`

- It uses positional placeholders `?,?,?,?` to associate the values to be inserted into the `students` table.


/// type=MS, answer=[2,3,4,5]

In `student.php`, which statements correctly describe `$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)");` on line 10?

- It executes the SQL statement.

- It prepares the SQL statement for execution.

- It returns the result set as a `PDOStatement` object.

- It calls the `prepare()` method of the `$conn` object.

- It assigns the `PDOStatement` object to the variable `$pstmt`.


/// type=MS, answer=[3,5]

Which statements correctly describe the `foreach` construct on line 11 of `student.php`?

- It displays all elements in `$row`.

- It accesses through each element in `$data`.

- It iterates through each element in the array.

- It creates and initializes the array variable `$data`.

- It assigns the value of the current element on each iteration to `$row`.


/// type=SS, answer=[2]

In `student.php`, what does the `execute()` method do on line 12?

- It executes the SQL statement.

- It executes the argument `$row`.

- It fetches the remaining row of the result set.

- It duplicates the values of `$data` to the SQL statement.

- It assigns the values of the multidimensional array `$data` to the variable `$row`.


/// type=SS, answer=[4]

What value is assigned to the variable `$row` on line 12 of `student.php`?

- The SQL statement.

- The DSN parameters.

- The `PDOStatment` object.

- The elements of the multidimensional array `$data`.

- The values of each key of `student1` and `student2`.


/// type=MS, answer=[2,3,4]

Which statements correctly describe `$pstmt->execute($row);` on line 12 of `student.php`?

- It queries the SQL statement.

- It returns the boolean value `true`.

- It calls the `execute()` method of the `$pstmt` object.

- It executes the argument `$row` in the `execute()` method.

- It assigns the returned value of the `execute()` method to the variable `$row`.


/// type=SS, answer=[3]

In `student.php`, what value is returned by `!$pstmt->execute($row)` on line 12?

- The SQL statement.

- The boolean value `true`.

- The boolean value `false`.

- The `PDOStatement` object.

- The elements of the multidimensional array `$data`.


/// type=SS, answer=[3]

Which statement correctly describes the code on lines 12, 13, and 14 of `student.php`?

- The statement displays the values assigned to the `$row` variable.

- The `if` statement evaluates to `true` and the statement on line 13 is executed.

- The `if` statement evaluates to `false` and the statement on line 13 is not executed.

- The `if` statement evaluates to `true` and it displays the string `Unable to insert values into the table.`.

- The `if` statement evaluates to `false` and it displays the string `Successfully inserted values into the table.`.


:::


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/PreparedStatement/InsertValuesDaronAlisaIntoStudentTable.sql]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'student1' => ['Daron', 'Guilliams', '2001-09-27', 'Male'],
        'student2' => ['Alisa', 'Ells', '1999-06-30', 'Female']
    );
     
    $sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (:first_name, :last_name, :birth_date, :gender)";

    try {
        $pstmt = $conn->prepare($sql);
        foreach ($data as $row) {
            if (!$pstmt->execute($row)) {
                throw new Exception("Unable to insert values into the table.");
            }
        }
        echo "Successfully inserted values into the table.";
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

- It prints `Successfully connected to the database.` and `Unable to insert values into the table.`.

- It prints `Successfully connected to the database.` and `Successfully inserted values into the table.`.


/// type=MS, answer=[1,2,3,4,5]

Which of the following are array values contained in the multidimensional array `$data`?

- `Daron`

- `Alisa`

- `Vikki`

- `Female`

- `1999-06-30`


/// type=SS, answer=[3]

How many elements does the multidimensional array `$data` have?

- 0

- 1

- 2

- 4

- 8


/// type=SS, answer=[1]

In `student.php`, what does `$sql` do on line 9?

- It holds the SQL statement.

- It executes the SQL statement.

- It holds the `PDOStatement` object.

- It holds the elements of the array variable `$data`.

- It stores the array values of the multidimensional array `$data`.


/// type=SS, answer=[4]

In `student.php`, which of the following represents the named placeholder as a parameter?

- `students`

- `INSERT INTO`

- `(first_name, last_name, birth_date, gender)`

- `(:first_name, :last_name, :birth_date, :gender)`

- `INSERT INTO students (first_name, last_name, birth_date, gender)`


/// type=SS, answer=[4]

In `student.php`, which named placeholder is associated with the value `1999-06-30` on line 9?

- `:gender`

- `:last_name`

- `birth_date`

- `:birth_date`

- `:first_name`


/// type=SS, answer=[5]

In `student.php`, which named placeholder is associated with the value `Daron` on line 9?

- `student1`

- `last_name`

- `first_name`

- `:last_name`

- `:first_name`


/// type=SS, answer=[5]

Which statement correctly describes `(first_name, last_name, birth_date, gender)` on line 9 of `student.php`?

- It locates the values in the SQL statement using positional placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender`.

- It assigns the named placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender` to be inserted into the `students` table.

- It sets the positional placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender` to replace the values in the SQL statement.

- It replaces the values in the SQL statement with named placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender` to have randomized values.

- It substitutes the values in the SQL statement with named placeholders `:first_name`, `:last_name`, `:birth_date`, and `:gender` to prevent from SQL injections.


/// type=MS, answer=[2,3,4,5]

Which statements correctly describe `$pstmt = $conn->prepare($sql)` on line 12 of `student.php`?

- It executes the SQL statement.

- It prepares the argument `$sql` for execution.

- It returns the result set as a `PDOStatement` object.

- It calls the `prepare()` method of the `$conn` object.

- It assigns the `PDOStatement` object to the variable `$pstmt`.


:::


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $pstmt = $conn->prepare("SELECT * FROM students WHERE gender = ?");
    $pstmt->execute(array('Female'));
    $data = $pstmt->fetchAll();
    
    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `2SamanthaDanes1999-10-12Female 4VikkiFernando2005-05-17Female `.

- It prints `Successfully connected to the database.` and `2SamanthaDanes1999-10-12Female 4VikkiFernando2005-05-17Female 6AlisaElls1999-06-30Female `.


/// type=MS, answer=[2,3,4,5]

Which statements correctly describe the code on line 4 of `student.php`?

- It queries the SQL statement.

- It returns the `PDOStatement` object.

- It calls the `prepare()` method of the `$conn` object.

- It assigns the `PDOStatement` object to the variable `$pstmt`.

- It prepares the SQL statement `SELECT * FROM students WHERE gender = ?` as an argument in the `prepare()` method.


/// type=SS, answer=[5]

Which statements correctly describe `WHERE gender = ?` on line 4 of `student.php`?

- It selects all columns in the `students` table.

- It deletes all columns in the `students` table whose gender is equal to `?`.

- It returns all records of students in the `students` table whose gender is equal to `?`.

- It updates all columns in the `students` table which contains a question mark `?` as gender.

- It uses the positional placeholder `?` to associate the value of `gender` to be filtered in the `students` table.


/// type=MS, answer=[1,3,5]

Which statements correctly describe `$pstmt->execute(array('Female'))` on line 5 of `student.php`?

- It returns the boolean value `true`.

- It holds the value `Female` in the SQL statement.

- It calls the `execute()` method of the `$pstmt` object.

- It assigns the specified value `Female` to the SQL statement.

- It executes the argument `array('Female')` in the `execute()` method.


/// type=SS, answer=[5]

In `student.php`, what does `$data` do on line 6?

- It holds the SQL statement.

- It executes the SQL statement.

- It stores the prepared statement.

- It connects to the PostgreSQL database.

- It holds the array of rows in the result set.


/// type=MS, answer=[2,3,5]

Which statements correctly describe the code on line 6 of `student.php`?

- It queries the SQL statement.

- It calls the `fetchAll()` method of the `$pstmt` object.

- It returns the array of the remaining rows in the result set.

- It executes the argument `$pstmt` in the `fetchAll()` method.

- It assigns the array of the remaining rows in the result set to the variable `$data`.


/// type=SS, answer=[4]

Which statement correctly describes `echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';` on line 6 of `student.php`?

- It assigns the values `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` to `$row`.

- It duplicates the values with the keys `student_id`, `first_name`, `last_name`, `birth_date`, and `gender`.

- It returns the values with the keys `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` from `$row`.

- It displays the values with the keys `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` from `$row`.

- It accesses the values `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` from the `students` table.


:::


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/PreparedStatement/UpdateFemaleGender.sql]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'gender' => 'F',
        'female_gender' => 'Female'
    );
    
    try {
        $sql = "UPDATE students SET gender = :gender WHERE gender = :female_gender";
        $pstmt = $conn->prepare($sql);
        if (!$pstmt->execute($data)) {
            throw new Exception("Unable to update values in the table.");
        }
        echo "Successfully updated values in the table.";
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

- It prints `Successfully connected to the database.` and `Unable to update values in the table.`.

- It prints `Successfully connected to the database.` and `Successfully updated values in the table.`.


/// type=SS, answer=[4]

Which statement correctly describes the code on lines 4, 5, 6, and 7 of `student.php`?

- It adds the associative array named `$data` to the database.

- It holds one value in each key of `gender` and `female_gender`.

- It accesses the elements of `$data` using the `array()` construct.

- It creates the associative array named `$data` with two keys `gender` and `female_gender`.

- It creates the associative array named `$data` with two elements `gender` and `female_gender`.


/// type=MS, answer=[4,5]

Which statements correctly describe `UPDATE students SET gender = :gender WHERE gender = :female_gender` on line 10 of `student.php`?

- It modifies all rows in the `gender` column.

- It selects the `students` table to be deleted.

- It selects the `students` table to be modified.

- It updates the rows in the `gender` column with the value of the named placeholder `:gender`.

- It sets the condition that all rows containing values equal to the value of the named placeholder `:female_gender` are updated.

:::


:::

/// type=REPL, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $pstmt = $conn->prepare("SELECT * FROM students WHERE gender = ?");
    $pstmt->execute(array('Female'));
    $data = $pstmt->fetchAll();
    
    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```
/// type=SS, answer=[4]

In the statement `$pstmt->execute(array('Female'));` on line 5 of `student.php`, replace the value `Female` with `F`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `2SamanthaDanes1999-10-12F 4VikkiFernando2005-05-17F 6AlisaElls1999-06-30F`.

- It prints `Successfully connected to the database.` and `1JohnSmith1999-02-10Male 3BerryMeisner2002-09-09Male 5DaronGuilliams2001-09-27Male`.

:::

:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/PreparedStatement/UpdateMaleGender.sql]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    try {
        $sql = "UPDATE students SET gender = ? WHERE gender = ?";
        $pstmt = $conn->prepare($sql);
        if (!$pstmt->execute(array('M', 'Male'))) {
            throw new Exception("Unable to update values in the table.");
        }
        echo "Successfully updated values in the table.";
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

- It prints `Successfully connected to the database.` and `Unable to update values in the table.`.

- It prints `Successfully connected to the database.` and `Successfully updated values in the table.`.


/// type=MS, answer=[4,5]

Which statements correctly describe `UPDATE students SET gender = ? WHERE gender = ?` on line 5 of `student.php`?

- It modifies all rows in the `gender` column.

- It selects the `students` table to be deleted.
 
- It selects the `students` table to be modified.

- It updates the rows in the `gender` column with the value of the positional placeholder `?`.

- It sets the condition that all rows containing values equal to the value of the positional placeholder `?` are updated.


/// type=MS, answer=[1,3,5]

Which statements correctly describe `$pstmt->execute(array('M', 'Male'))` on line 7 of `student.php`?

- It returns the boolean value `true`.

- It holds the values `M` and `Male` in the SQL statement.

- It calls the `execute()` method of the `$pstmt` object.

- It assigns the specified values `M` and `Male` to the SQL statement.

- It executes the argument `array('M', 'Male')` in the `execute()` method.


:::


:::

/// type=REPL, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $pstmt = $conn->prepare("SELECT * FROM students WHERE gender = ?");
    $pstmt->execute(array('Male'));
    $data = $pstmt->fetchAll();
    
    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```
/// type=SS, answer=[4]

In the statement `$pstmt->execute(array('Male'));` on line 5 of `student.php`, replace the value `Male` with `M`. Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database. ` and `1JohnSmith1999-02-10M 3BerryMeisner2002-09-09M 5DaronGuilliams2001-09-27M`.

- It prints `Successfully connected to the database. ` and `2SamanthaDanes1999-10-12F 4VikkiFernando2005-05-17F 6AlisaElls1999-06-30F`.

:::


+++


+++

### Part 2: Knowledge Assessment

/// type=MS, answer=[1,5]

Which statements correctly describe `PDO::prepare()`?

- It prepares an SQL statement.

- It sends queries to databases.

- It stores the values in an array.

- It executes a prepared statement.

- It returns a `PDOStatement` object.


/// type=SS, answer=[2]

What argument is passed in the `PDO::prepare()` method?

- A DSN parameter.

- An SQL statement.

- An array of values.

- An `echo` statement.

- A `PDOStatement` object.


/// type=SS, answer=[4]

Which statement correctly describes `PDOStatement::execute()`?

- It prepares an SQL statement.

- It sends queries to databases.

- It stores the values in an array.

- It executes a prepared statement.

- It returns a `PDOStatement` object.


/// type=SS, answer=[3]

What argument is passed in the `PDO::execute()` method?

- A DSN parameter.

- An SQL statement.

- An array of values.

- An `echo` statement.

- A `PDOStatement` object.


/// type=MS, answer=[3,4]

Which types of placeholders are supported by the prepared statement?

- DSN parameters

- Array variables

- Named placeholders

- Positional placeholders

- Predefined placeholders


/// type=SS, answer=[5]

Which statements correctly describe a prepared statement?

- It is used to alter SQL commands.

- It prepares an SQL statement for execution

- It sends queries and uploads data to databases. 

- It substitutes the actual parameter values with placeholders.

- It is used to execute an SQL statement multiple times with the same or different parameter values.


/// type=SS, answer=[5]

Which statement correctly describes an SQL injection?

- It is a method fetches large result sets.

- It is a method that prepares an SQL statement.

- It is a method that executes a prepared statement.

- It is an SQL template that contains placeholders.

- It is a code injection technique that alters SQL commands and exposes hidden data.


+++


+++

### Part 3: Finding and Fixing Errors

:::

/// type=REPL, readonly=true, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
        'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
    );
     
    try {
        $pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender)");
        foreach ($data as $row) {
            if (!$pstmt->execute($row)) {
                throw new Exception("Unable to insert values into the table.");
            }
        }
        echo "Successfully inserted values into the table.";
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

- It prints `Successfully connected to the database.` and `Unable to insert values into the table.`.

- It prints `Successfully connected to the database.` and `Successfully inserted values into the table.`.


/// type=MS, answer=[4,5]

Which statements correctly describe the error message?

- There are no parentheses `()` that enclosed the SQL statement on line 10.

- In `student.php`, there is no semicolon `;` at the end of the statement on line 7.

- On line 10, the column names `first_name`, `last_name`, `birth_date`, and `gender` are not enclosed in single quotes `''`.

- In `student.php`, there is no `VALUES` clause that specifies the values to be inserted into the selected columns on line 10.

- On line 10, the statement `$pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender)");` is incorrect.

:::


/// type=CR, answer=[tests/PreparedStatement/MissingValuesClause.php], filename=[connection.php,student.php]

Correct the code so that it inserts values using the `VALUES` clause with positional placeholders as parameters and outputs the strings `Successfully connected to the database.` and `Successfully inserted values into the table.`.

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'student1' => ['Berry', 'Meisner', '2002-09-09', 'Male'],
        'student2' => ['Vikki', 'Fernando', '2005-05-17', 'Female']
    );
     
    try {
        $pstmt = $conn->prepare("INSERT INTO students (first_name, last_name, birth_date, gender)");
        foreach ($data as $row) {
            if (!$pstmt->execute($row)) {
                throw new Exception("Unable to insert values into the table.");
            }
        }
        echo "Successfully inserted values into the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'min_birth_date' => '1999-01-01',
        'max_birth_date' => '2000-01-01'
    );
    
    $sql = "SELECT * FROM students WHERE birth_date >= ':min_birth_date' AND birth_date < ':max_birth_date'";
    $pstmt = $conn->prepare($sql);
    $pstmt->execute($data);
    $data = $pstmt->fetchAll();

    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```
/// type=SS, answer=[4]

Execute the program. What is the error message?

- Undefined variable: `sql` on line 11

- syntax error, unexpected `$pstmt` on line 11

- syntax error, unexpected `students` on line 9

- Invalid parameter number: `:min_birth_date` on line 11

- `PDO::prepare()` expects at least `1` parameter, `0` given on line 10


/// type=MS, answer=[4,5]

Which statements correctly describe the error?

- On line 9, the SQL statement is not enclosed in double quotes `""`.

- In `student.php`, the semicolon `;` and close parenthesis `)` are misplaced on line 7.

- On lines 5 and 6, the values set by the keys `:min_birth_date` and `:max_birth_date` is incorrect.

- On line 9, the named placeholders `:min_birth_date` and `:max_birth_date` are enclosed in single quotes `''`.

- On line 9, the statement `$sql = "SELECT * FROM students WHERE birth_date >= ':min_birth_date' AND birth_date < ':max_birth_date'";` is incorrect.

:::

/// type=CR, answer=[tests/PreparedStatement/NamedPlaceholdersEnclosedinSingleQuotes.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `1JohnSmith1999-02-10M 2SamanthaDanes1999-10-12F 6AlisaElls1999-06-30F`.

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. <br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'min_birth_date' => '1999-01-01',
        'max_birth_date' => '2000-01-01'
    );
    
    $sql = "SELECT * FROM students WHERE birth_date >= ':min_birth_date' AND birth_date < ':max_birth_date'";
    $pstmt = $conn->prepare($sql);
    $pstmt->execute($data);
    $data = $pstmt->fetchAll();

    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database.<br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    try {
        $sql = "UPDATE students SET gender = :? WHERE gender = :?";
        $pstmt = $conn->prepare($sql);
        if (!$pstmt->execute(array('F', 'Female'))) {
            throw new Exception("Unable to update values in the table.");
        }
        echo "Successfully updated values in the table.";
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

- It prints `Successfully connected to the database.` and `Unable to update values in the table.`.

- It prints `Successfully connected to the database.` and `Successfully updated values in the table.`.


/// type=MS, answer=[4,5]

Which statements correctly describe the error message?

- There are no parentheses `()` that enclosed the SQL statement on line 5.

- On line 5, the column name `gender` is not enclosed in single quotes `''`.

- In `student.php`, the colon `:` and positional placeholder `?` are misplaced on line 5.

- On line 5, the statement `$sql = "UPDATE students SET gender = :? WHERE gender = :?";` is incorrect.

- On line 5, the positional placeholders in `SET gender = :?` and `WHERE gender = :?` contain a colon `:`.

:::


/// type=CR, answer=[tests/PreapredStatement/ArgumentErrorContainsAColon.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully updated values in the table.`.

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database.<br />";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    try {
        $sql = "UPDATE students SET gender = :? WHERE gender = :?";
        $pstmt = $conn->prepare($sql);
        if (!$pstmt->execute(array('F', 'Female'))) {
            throw new Exception("Unable to update values in the table.");
        }
        echo "Successfully updated values in the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'student1' => ['Daron', 'Guilliams', '2001-09-27', 'Male'],
        'student2' => ['Alisa', 'Ells', '1999-06-30', 'Female']
    );
     
    $sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (first_name, last_name, birth_date, gender)";

    try {
        $pstmt = $conn->prepare($sql);
        foreach ($data as $row) {
            if (!$pstmt->execute($row)) {
                throw new Exception("Unable to insert values into the table.");
            }
        }
        echo "Successfully inserted values into the table.";
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

- It prints `Successfully connected to the database.` and `Unable to insert values into the table.`.

- It prints `Successfully connected to the database.` and `Successfully inserted values into the table.`.


/// type=MS, answer=[3,5]

Which statements correctly describe the error message?

- On line 9, the `INSERT INTO` statement is incorrect.

- There are no parentheses `()` that enclosed the SQL statement on line 9.

- There is no colon `:` in the specified named placeholders inside the `VALUES` clause on line 9.

- On line 9, the column names `first_name`, `last_name`, `birth_date`, and `gender` are not enclosed in single quotes `''`.

- On line 9, the statement `$sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (first_name, last_name, birth_date, gender)";` is incorrect.

:::


/// type=CR, answer=[tests/PreparedStatement/MissingColonNamedPlaceholders.php], filename=[connection.php,student.php]

Correct the code so that it outputs the string `Successfully connected to the database.` and `Successfully inserted values into the table.`.

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $data = array(
        'student1' => ['Daron', 'Guilliams', '2001-09-27', 'Male'],
        'student2' => ['Alisa', 'Ells', '1999-06-30', 'Female']
    );
     
    $sql = "INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (first_name, last_name, birth_date, gender)";

    try {
        $pstmt = $conn->prepare($sql);
        foreach ($data as $row) {
            if (!$pstmt->execute($row)) {
                throw new Exception("Unable to insert values into the table.");
            }
        }
        echo "Successfully inserted values into the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $sql = "SELECT * FROM students WHERE gender = ?";

    $pstmt = $conn->prepare();
    $pstmt->execute(array('F'));
    $data = $pstmt->fetchAll();
    
    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```
/// type=MS, answer=[4,5]

Execute the program. What are the error messages?

- Undefined variable: `pstmt` on line 7

- Undefined variable: `data` on line 10

- Invalid argument supplied for `foreach()` on line 10

- `PDO::prepare()` expects at least `1` parameter, `0` given on line 6

- Uncaught Error: Call to a member function `execute()` on boolean on line 7


/// type=MS, answer=[2,5]

Which statements correctly describe the error?

- On line 4, the `students` table does not exist.

- On line 6, the statement `$pstmt = $conn->prepare();` is incorrect.

- In `student.php`, there is no semicolon `;` at the end of the statement on line 4.

- In `student.php`, there is no close parenthesis `)` at the end of the statement on line 7.

- There is no argument `$sql` specified in the statement `$pstmt = $conn->prepare();` on line 6.

:::


/// type=CR, answer=[tests/DataObjects/MissingArgumentInPrepare.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `2SamanthaDanes1999-10-12F 4VikkiFernando2005-05-17F 6AlisaElls1999-06-30F`.

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    try {
        $conn = new PDO("pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password");
        if ($conn) {
            echo "Successfully connected to the database. ";
        }
    } catch (Exception $e) {
        echo "Unable to establish a connection."; 
    }
?>
```

```php
// student.php
<?php
    require_once("connection.php");

    $sql = "SELECT * FROM students WHERE gender = ?";

    $pstmt = $conn->prepare();
    $pstmt->execute(array('F'));
    $data = $pstmt->fetchAll();
    
    foreach ($data as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```

+++


+++

### Part 4: Practice

/// type=CR, answer=[tests/PreparedStatement/CreatePHPProgramUsingPrepareAndExecute.php], init=[commands/DataObjects/InsertTwoStudentDataIntoTableStudents.sql], filename=[connection.php,student.php]

Write a program that uses two PHP files named `connection.php` and `student.php` to insert two student data into the `students` table. First, write a PHP file named `connection.php` that uses the `PDO_PGSQL` driver, `PDO_PGSQL DSN`, and `PDO` class to connect to the PostgreSQL database. Create the variables `$host`, `$db`, `$port`, `$username`, and `$password`. Assign the values `localhost`, `LibraryDB`, `5432`, `postgres`, and `Admin01` to the variables respectively. Then, assign the `PDO_PGSQL DSN` statement which contains the DSN parameters `host`, `port`, `dbname`, `username`, and `password` to the `$dsn` variable. Set the DSN parameters with their respective values `$host`, `$db`, `$port`, `$username`, and `$password`. Add the `try` and `catch` statements. Inside the `try` block, add a statement that creates the `$conn` object an instance of the `PDO` class which passes the argument `$dsn`. Then, add the `if` statement to evaluate the `$conn` object inside the parentheses `()`. Inside the `if` block, add an `echo` statement to display the string `Successfully connected to the database.`. Inside the `catch` block, add an `echo` statement to display the error message `Unable to establish a connection.` if an exception occurs within the `try` block.

Next, write a PHP file named `student.php`. Add the `require_once()` statement to have the `connection.php` file included. Create an array variable named `$data` and assign the elements `'student1' => ['Carlo', 'Pears', '1998-04-04', 'M']` and `'student2' => ['Genevie', 'Lieser', '1996-05-25', 'F']` using the `array()` construct. Then, add a statement that assigns the SQL statement `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES (?,?,?,?)` to the `$sql` variable. Add the `try` and `catch` statements. Inside the `try` block, add a statement that assigns the `prepare()` method call of the `$conn` object which passes the argument `$sql` to the `$pstmt` variable. Then, add the `foreach` statement that iterates through each element in `$data` and assigns the value of the current element on each iteration to `$row`. Inside the `foreach` statement, add the `if` statement that evaluates the negated statement `$pstmt->execute($row)` inside the parentheses `()`. Inside the `if` block, add a statement that throws an exception message `Unable to insert values into the table.`. After the `if` block, add the `echo` statement that displays the string `Successfully inserted values into the table.`. Then, inside the `catch` block, add the statement `echo $e->getMessage();`. Run the program to view the output.

```php
// connectiion.php
<?php

?>
```

```php
// student.php
<?php

?>
```

+++