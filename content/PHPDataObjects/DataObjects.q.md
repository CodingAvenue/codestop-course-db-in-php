# PHP Data Objects

+++

### Part 1: Sample Code Analysis

:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/DataObjects/CreateTableStudents.sql]

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
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

    $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";
    
    try {
        $stmt = $conn->query($sql);
        if (!$stmt) {
            throw new Exception("Unable to create a table.");
        }
        echo "Successfully created a table."; 
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

- It prints `Unable to establish a connection.` and `Successfully created a table.`.

- It prints `Successfully connected to the database.` and `Successfully created a table.`.


/// type=MS, answer=[3,4,5]

Which of the following are DSN parameter values? 

- `$sql`

- `$conn`

- `postgres`

- `localhost`

- `LibraryDB`


/// type=SS, answer=[4]

What is the name of the database?

- `Admin01`

- `postgres`

- `localhost`

- `LibraryDB`

- `student_info`


/// type=SS, answer=[3]

In `connection.php`, what is `psql:` in the statement `pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password` on line 8?

- It is the hostname.

- It is the table name.

- It is the DSN prefix.

- It is the SQL statement.

- It is the database name.


/// type=MS, answer=[4,5]

Which statements correctly describe the code on line 11 of `connection.php`?

- It sets the value of `$dsn` to `PDO()`.

- It assigns `PDO($dsn)` to the `$conn` object.

- It evaluates the `$conn` object of the `PDO` class.

- It creates the `$conn` object as an instance of the `PDO` class.

- It passes the `$dsn` variable as an argument of the `PDO` class.


/// type=SS, answer=[5]

In `connection.php`, what does the statement `"pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password"` do on line 8?

- It holds the `PDOStatement` class.

- It represents a prepared statement.

- It sends queries or uploads data to databases.

- It creates a new table in the PostgreSQL database.

- It represents the `PDO_PGQSQL DSN` statement that connects to the PostgreSQL database.


/// type=SS, answer=[3]

In `student.php`, what does the statement `require_once("connection.php");` do on line 2?

- It updates the file `connection.php`.

- It establishes a connection to the PostgreSQL database.

- It includes the file `connection.php` in the file `student.php`.

- It removes the file `connection.php` in the file `student.php`.

- It excludes the file `connection.php` in the file `student.php`.


/// type=SS, answer=[5]

In `student.php`, which statement correctly describes `CREATE TABLE IF NOT EXISTS` on line 4?

- The `CREATE TABLE IF NOT EXISTS` statement modifies an existing table.

- The `CREATE TABLE IF NOT EXISTS` statement creates a new database in the table.

- The `CREATE TABLE` statement uses the parameter `IF NOT EXISTS` to modifiy an existing table named `students.`.

- The `CREATE TABLE` statement uses the parameter `IF NOT EXISTS` to create a copy of existing tables named `students`.

- The `CREATE TABLE` statement uses the parameter `IF NOT EXISTS` to check if a table with the name `students` already exists.


/// type=SS, answer=[1]

In `student.php`, what does `$sql` do on line 4?

- It holds the SQL statement.

- It executes the SQL statement. 

- It holds the `PDOStatement` object.

- It connects to the PostgreSQL database.

- It stores the variables of the DSN parameters.


/// type=MS, answer=[2,3,4,5]

In `student.php`, which statements correctly describe `$stmt = $conn->query($sql);` on line 7?

- It connects to the PostgreSQL database.

- It calls the `query()` method of the `$conn` object.

- It returns the result set as a `PDOStatement` object.

- It executes the argument `$sql` in the `query()` method.

- It assigns the `PDOStatement` object to the variable `$stmt`.


/// type=SS, answer=[5]

What does the `if` construct do on line 8 of `student.php`?

- It adds the value of `$stmt`.

- It displays the value of `$stmt`.

- It removes the value of `$stmt`.

- It assigns a value to the `$stmt` variable.

- It evaluates the negated value of `$stmt` inside the parentheses `()`.


/// type=SS, answer=[3]

In `student.php`, what does `$stmt` do on line 7?

- It holds the SQL statement.

- It executes the SQL statement. 

- It holds the `PDOStatement` object.

- It connects to the PostgreSQL database.

- It carries the variables of the DSN parameters.


/// type=SS, answer=[3]

Which statement correctly describes the code on lines 8, 9, and 10 of `student.php`?

- The statement displays the values assigned to the `$stmt` variable.

- The `if` statement evaluates to `true` and the statement on line 9 is executed.

- The `if` statement evaluates to `false` and the statement on line 9 is not executed.

- The `if` statement evaluates to `true` and it displays the string `Unable to create a table.`.

- The `if` statement evaluates to `false` and it displays the string `Successfully created a table.`.


/// type=SS, answer=[2]

What is the name of the table created?

- `Admin01`

- `students`

- `postgres`

- `LibraryDB`

- `students_id`


/// type=MS, answer=[1,2,3,4,5]

What are the column names in the `students` table?

- `gender`

- `birth_date`

- `last_name`

- `first_name`

- `student_id`


/// type=SS, answer=[5]

Which statement correctly describes the code on lines 12, 13, and 14 of `student.php`?

- It creates a new `Exception` class.

- It updates the `Exception` message thrown.

- It adds an exception in the statement `echo $e->getMessage()`.

- It removes an exception using the statement `echo $e->getMessage();`.

- It executes the `echo` statement if an exception occurs within the `try` block.

:::


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/DataObjects/InsertJohnSmith.sql]

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

    try {
        $stmt = $conn->query("INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')");
        if (!$stmt) {
            throw new Exception("Unable to insert values into the table.");
        }
        echo "Successfully inserted the values into the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`

- It prints `Successfully connected to the database.` and `Unable to insert values into the table.`.

- It prints `Successfully connected to the database.` and `Successfully inserted the values into the table.`.


/// type=MS, answer=[4,5]

Which statements correctly describe the code on line 9 of `connection.php`?

- It evaluates the `$conn` object.

- It sets the `PDO` class to the `PDO_PGQSL DSN` statement

- It assigns the `PDO_PGQSL DSN` statement to the `PDO` class.

- It creates the `$conn` object as an instance of the `PDO` class.

- It passes the `PDO_PGQSL DSN` statement as an argument of the `PDO` class.


/// type=MS, answer=[1,2,3,5]

What values are inserted by the statement `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')")` on line 5?

- `Male`

- `John`

- `Smith`

- `first_name`

- `1999-02-10`


/// type=SS, answer=[5]

In `student.php`, what does the query `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')")` do on line 5?

- It modifies multiple tables.

- It adds three columns in the `students` table.

- It inserts one column into the `students` table.

- It modifies the values `John`, `Smith`, `1999-02-10`, and `Male` in the `students` table.

- It adds a new row that contains the values `John`, `Smith`, `1999-02-10`, and `Male` in the `students` table.


/// type=MS, answer=[2,3,4,5]

Which statements correctly describe the code on line 5 of `student.php`?

- It connects to the PostgreSQL database.

- It calls the `query()` method of the `$conn` object.

- It returns the result set as a `PDOStatement` object.

- It assigns the `PDOStatement` object to the variable `$stmt`.

- It executes the argument `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')")` in the `query()` method.


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

    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
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

    $stmt = $conn->query("SELECT * FROM students");
    foreach ($stmt as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `JohnSmith1999-10-02Male`.

- It prints `Successfully connected to the database.` and `1JohnSmith1999-02-10Male`.


/// type=MS, answer=[3,5]

Which statements correctly describe the `foreach` construct on line 5 of `student.php`?

- It removes all the elements in `$stmt`.

- It accesses all the elements in `$stmt`.

- It iterates through each element in the array.

- It removes all the elements in the multidimensional array `$stmt`.

- It assigns the value of the current element on each iteration to `$row`.


/// type=SS, answer=[2]

What value is assigned to `student_id`?

- `0`

- `1`

- `John`

- `Smith`

- No value is assigned.


/// type=MS, answer=[3,4,5]

Which statements correctly describe `$stmt = $conn->query("SELECT * FROM students");` on line 4 of `student.php`?

- It assigns the value of `$conn` to `$stmt`.

- It ends the execution of the `query()` method. 

- It calls the `query()` method of the `$conn` object.

- It assigns the result set as a `PDOStatement` object to the variable `$stmt`.

- It executes the argument `SELECT * FROM students` in the `query()` method.


/// type=SS, answer=[5]

In `student.php`, which statement correctly describes `echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender']. ' ';` on line 6?

- It assigns the values `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` to `$row`.

- It accesses the values `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` from the `students` table.

- It duplicates the value of the array element with the keys `student_id`, `first_name`, `last_name`, `birth_date`, and `gender`.

- It returns the value of the array element with the keys `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` from `$row`.

- It displays the returned value of the array element with the keys `student_id`, `first_name`, `last_name`, `birth_date`, and `gender` from `$row`.


:::


+++


+++

### Part 2: Knowledge Assessment

/// type=MS, answer=[2,5]

Which statements correctly describe `PDO::query()`?

- It sends queries or uploads data to certain databases.

- It executes an SQL statement in a single function call.

- It defines an interface in PHP to access certain databases.

- It represents a connection between a database server and PHP.

- It returns a result set as a `PDOStatement` object or `false` on failure.


/// type=SS, answer=[2]

What argument is passed in the `PDO::query()` method?

- A DSN parameter.

- An SQL statement.

- An `echo` statement.

- A `PDOStatement` object.

- A `PDO_PGQSL DSN` statement.


/// type=SS, answer=[5]

What value does the `PDO::query()` method return?

- A DSN parameter.

- An SQL statement.

- A `PDO_PGSQL DSN` statement.

- A `true` or `false` boolean value.

- A `PDOStatement` object or `false` on failure.


/// type=MS, answer=[4,5]

Which statements correctly describe a `PDOStatement`?

- It defines an interface in PHP.

- It sends queries to the database.

- It executes a prepared statement.

- It returns an associated result set.

- It represents a prepared statement.


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
    
    try {
        $stmt = $conn->query(CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10)));
        if (!$stmt) {
            throw new Exception("Unable to create a table.");
        } 
        echo "Successfully created a table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is the error message?

- syntax error, unexpected `=` on line 5

- syntax error, unexpected `if` (T_IF) on line 6

- syntax error, unexpected `TABLE` (T_STRING) on line 5

- syntax error, unexpected `:`, expecting `,` or `)` on line 5

- syntax error, unexpected `TABLE` (T_STRING), expecting `,` or `)` on line 5


/// type=MS, answer=[3,4]

Which statements correctly describe the error?

- There is no column name specified before `VARCHAR(80)` on line 5.

- In `student.php`, there is no comma `,` at the end of the statement on line 5.

- In `student.php`, the SQL statement is not enclosed in double quotes `""` on line 5.

- On line 5, the statement `$stmt = $conn->query(CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10)));` is incorrect.

- There are no parentheses `()` that enclosed the statement `CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))`.

:::


/// type=CR, answer=[tests/DataObjects/MissingDoubleQuotesTest.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully created a table.`.

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
    
    try {
        $stmt = $conn->query(CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10)));
        if (!$stmt) {
            throw new Exception("Unable to create a table.");
        } 
        echo "Successfully created a table.";
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

    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
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

    $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";
    
    try {
        $stmt = query($sql);
        if (!$stmt) {
            throw new Exception('Unable to create a table.');
        }
        echo "Successfully created a table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=SS, answer=[4]

Execute the program. What is its output?

- No output is displayed.

- It prints `Successfully created a table.`.

- It prints `Unable to establish a connection`.

- It prints `Successfully connected to the database.` and produces an error.

- It prints `Successfully connected to the database.` and `Successfully created a table.`.


/// type=SS, answer=[4]

What is the error message?

- `Unable to create a table.`

- Undefined variable: `stmt` on line 8

- syntax error, unexpected `if` (T_IF) on line 8

- Uncaught Error: Call to undefined function `query()` on line 7

- `PDO::query()` expects at least `1` parameter, `0` given on line 7


/// type=MS, answer=[2,4]

Which statements best describe the error?

- The argument passed is `$sql` on line 7.

- On line 7, the statement `$stmt = query($sql);` is incorrect.

- There are no parentheses `()` that enclosed the SQL statement on line 4.

- In `student.php`, there are no `$conn` object and object operator `->` on line 7. 

- In `student.php`, the semicolon `;` and the close parenthesis `)` are misplaced on line 7. 

:::


/// type=CR, answer=[tests/DataObjects/MissingObjectAndOperatorTest.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully created a table.`.

```php
// connection.php
<?php
    $host = 'localhost';
    $db = 'LibraryDB';
    $port = '5432';
    $username = 'postgres';
    $password = 'Admin01';

    $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

    try {
        $conn = new PDO($dsn);
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

    $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";
    
    try {
        $stmt = query($sql);
        if (!$stmt) {
            throw new Exception('Unable to create a table.');
        }
        echo "Successfully created a table.";
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

  $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

  try {
      $conn = new PDO($dsn);
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

    $sql = "INSERT students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')";

    try {
        $stmt = $conn->query($sql);
        if (!$stmt) {
            throw new Exception('Unable to insert values into the table.');
        }
        echo "Successfully inserted the values into the table.";   
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

- It prints `Successfully connected to the database.` and `Successfully inserted the values into the table.`.


/// type=MS, answer=[2,5]

Which statements correctly describe the error message?

- On line 4, the `students` table does not exist.

- The `INSERT INTO` statement is miswritten as `INSERT` on line 4.

- There is no comma `,` between the values `John` and `Smith` on line 4.

- On line 4, the table name `students` is not allowed in an `INSERT` statement.

- On line 4, the SQL statement `INSERT students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')` is incorrect.

:::


/// type=CR, answer=[tests/DataObjects/InvalidSQLStatementTest.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully inserted the values into the table.`.

```php
// connection.php
<?php
  $host = 'localhost';
  $db = 'LibraryDB';
  $port = '5432';
  $username = 'postgres';
  $password = 'Admin01';

  $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

  try {
      $conn = new PDO($dsn);
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

    $sql = "INSERT students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')";

    try {
        $stmt = $conn->query($sql);
        if (!$stmt) {
            throw new Exception('Unable to insert values into the table.');
        }
        echo "Successfully inserted the values into the table.";   
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, filename=[connection.php,student.php], init=[commands/DataObjects/InsertSamanthaDanes.sql]

```php
// connection.php
<?php
  $host = 'localhost';
  $db = 'LibraryDB';
  $port = '5432';
  $username = 'postgres';
  $password = 'Admin01';

  $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

  try {
      $conn = new PDO($dsn);
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

    $sql = "INSERT INTO students (first_name, last_name, birth_date, gender)";

    try {
        $stmt = $conn->query($sql);
        if (!$stmt) {
            throw new Exception('Unable to insert values into the table.');
        }
        echo "Successfully inserted the values into the table.";
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

- It prints `Successfully connected to the database.` and `Successfully inserted the values into the table.`.


/// type=MS, answer=[4,5]

Which statements correctly describe the error message?

- On line 4, the `students` table does not exist.

- There are no parentheses `()` that enclosed the SQL statement on line 4.

- on line 4, the strings `first_name`, `last_name`, `birth_date`, and `gender` are not enclosed in single quotes `''`.

- In `student.php`, there is no `VALUES` clause that specifies the values to be inserted into the selected columns on line 4.

- On line 4, the statement `$sql = "INSERT INTO students (first_name, last_name, birth_date, gender)";` is incorrect.

:::

/// type=CR, answer=[tests/DataObjects/MissingValuesClause.php], filename=[connection.php,student.php]

Correct the code so that it inserts the values `Samantha`, `Danes`, `1999-10-12`, and `Female` into the table and displays the strings `Successfully connected to the database.` and `Successfully inserted the values into the table.`. 

```php
// connection.php
<?php
  $host = 'localhost';
  $db = 'LibraryDB';
  $port = '5432';
  $username = 'postgres';
  $password = 'Admin01';

  $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

  try {
      $conn = new PDO($dsn);
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

    $sql = "INSERT INTO students (first_name, last_name, birth_date, gender)";

    try {
        $stmt = $conn->query($sql);
        if (!$stmt) {
            throw new Exception('Unable to insert values into the table.');
        }
        echo "Successfully inserted the values into the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```

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

  $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

  try {
      $conn = new PDO($dsn);
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

    $stmt = $conn->query("SELECT * FROM students");
    foreach ($stmt as $row) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender'].' ';
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `2SamanthaDanes1999-10-12Female`.

- It prints `Successfully connected to the database.` and `1JohnSmith1999-02-10Male 2SamanthaDanes1999-10-12Female`.


/// type=SS, answer=[2]

In `student.php`. remove `as $row` in the `foreach` statement on line 5. Execute the program. What is the error message?

- Undefined variable: `row` on line 5

- syntax error, unexpected `)` on line 5

- syntax error, unexpected `foreach` on line 5

- Invalid argument supplied for `foreach()` on line 5 

- syntax error, unexpected `}`, expecting the end of file on line 5


/// type=SS, answer=[5]

Which statement correctly describes the error?

- The `students` table is miswritten as `student` on line 4.

- In `student.php`, there is no open curly brace `{` on line 5.

- On line 5, the argument `$stmt` in the `foreach` construct is invalid.

- The name of the database is not included in the `SELECT` statement on line 4.

- In `student.php`, the value of the current element on each iteration is not assigned to a variable on line 5.

:::


/// type=CR, answer=[tests/DataObjects/IncorrectForeachStatement.php], filename=[connection.php,student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `1JohnSmith1999-02-10Male 2SamanthaDanes1999-10-12Female`.

```php
// connection.php
<?php
  $host = 'localhost';
  $db = 'LibraryDB';
  $port = '5432';
  $username = 'postgres';
  $password = 'Admin01';

  $dsn = "pgsql:host=$host;port=$port;dbname=$db;user=$username;password=$password";

  try {
      $conn = new PDO($dsn);
      if ($conn) {
          echo "Successfully connected to the database. ";
      }
  } catch (Exception $e) {
      echo "Unable to establish a connection."; 
  }
?>
```

```php
<?php
    require_once("connection.php");

    $stmt = $conn->query("SELECT * FROM students");
    foreach ($stmt) {
        echo $row['student_id'].$row['first_name'].$row['last_name'].$row['birth_date'].$row['gender'].' ';
    }
?>
```

+++


+++

### Part 4: Practice

/// type=CR, answer=[tests/DataObjects/CreatePHPProgramUsingQueryMethodTest.php], init=[commands/DataObjects/UpdateStudentsTable.sql], filename=[connection.php,student.php]

Write a program that uses two php files named `connection.php` and `student.php` to update a value in the `students` table. First, write a PHP file named `connection.php` that uses the `PDO_PGSQL` driver, `PDO_PGSQL DSN`, and `PDO` class to connect to the PostgreSQL database. Create the variables `$host`, `$db`, `$port`, `$username`, and `$password`. Assign the values `localhost`, `LibraryDB`, `5432`, `postgres`, and `Admin01` to the variables respectively. Then, assign the `PDO_PGSQL DSN` statement which contains the DSN parameters `host`, `port`, `dbname`, `username`, and `password` to the `$dsn` variable. Set the DSN parameters with their respective values `$host`, `$db`, `$port`, `$username`, and `$password`. Add the `try` and `catch` statements. Inside the `try` block, add a statement that creates the `$conn` object an instance of the `PDO` class which passes the argument `$dsn`. Then, add the `if` statement to evaluate the `$conn` object inside the parentheses `()`. Inside the `if` block, add an `echo` statement to display the string `Successfully connected to the database.`. Inside the `catch` block, add an `echo` statement to display the error message `Unable to establish a connection.` if an exception occurs within the `try` block.

Next, write a PHP file named `student.php`. Add the `require_once()` statement to have the `connection.php` file included. Then, assign the SQL statement `UPDATE students SET gender = 'M' where gender = 'Male'` to the `$sql` variable. Add the `try` and `catch` statements. Inside the `try` block, assign the `query()` method of the `$conn` object which passes the argument `$sql` to the `$stmt` variable. Then, add the `if` statement that evaluates the negated value of `$stmt` inside the parentheses `()`. Inside the `if` block, add a statement that throws an exception message `Unable to update values in the table.`. After the `if` block, add the `echo` statement that displays the string `Successfully updated values in the table.`. Inside the `catch` block, add the statement `echo $e->getMessage();`. Run the program to view the output.

```php
// connection.php
<?php

?>
```

```php
// student.php
<?php

?>
```

+++