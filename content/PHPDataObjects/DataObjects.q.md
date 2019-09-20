# PHP Data Objects

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "CREATE TABLE IF NOT EXISTS students (student_id SERIAL, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10), PRIMARY KEY (student_id))";

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


/// type=MS, answer=[3,4,5], init=[commands/DataObjects/CreateTableStudents.sql]

Which of the following are DSN parameter values? 

- `$sql`

- `$conn`

- `codestop`

- `localhost`

- `LibraryDB`


/// type=SS, answer=[4]

What is the name of the database?

- `Admin01`

- `codestop`

- `localhost`

- `LibraryDB`

- `student_info`


/// type=SS, answer=[3]

In `Connection.php`, what is `psql:` in the statement `pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD` on line 13?

- It is the hostname.

- It is the table name.

- It is the DSN prefix.

- It is the SQL statement.

- It is the database name.


/// type=SS, answer=[3]

In `Connection.php`, what does `self::HOST` do on line 13?

- It creates the `HOST` constant.

- It defines the `HOST` constant.

- It accessess the value of `HOST`.

- It evaluates the value of `HOST`.

- It replicates the values of `HOST`.


/// type=SS, answer=[3]

What value is associated with `self::USERNAME` on line 13 of `Connection.php`?

- `5432`

- `Admin01`

- `codestop`

- `localhost`

- `LibraryDB`


/// type=MS, answer=[3,4,5]

Which statements correctly describe the code on line 13 of `Connection.php`?

- It sets the values to return.

- It passes the values as an argument.

- It returns the result set as a `PDOStatement` object.

- It creates the object as an instance of the `PDO` class.

- It contains the DSN parameters to establish a connection to the PostgreSQL database.


/// type=SS, answer=[5]

In `Connection.php`, what does the statement `"pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD` do on line 13?

- It holds the `PDOStatement` class.

- It represents a prepared statement.

- It sends queries or uploads data to databases.

- It creates a new table in the PostgreSQL database.

- It represents the `PDO_PGQSQL DSN` statement that connects to the PostgreSQL database.


/// type=SS, answer=[3]

In `Student.php`, what does the statement `require_once("./Connection.php");` do on line 2?

- It updates the file `Connection.php`.

- It establishes a connection to the PostgreSQL database.

- It includes the file `Connection.php` in the file `Student.php`.

- It removes the file `Connection.php` in the file `Student.php`.

- It excludes the file `Connection.php` in the file `Student.php`.


/// type=MS, answer=[1,2]

In `Student.php`, which statements correctly describe `CREATE TABLE IF NOT EXISTS` on line 6?

- It checks if the `students` table does not exist in the `LibraryDB` database.

- It creates the `students` table if it does not exist in the `LibraryDB` database.

- It creates the `students` table if it already exists in the `LibraryDB` database.

- It modifies the `students` table if it does not exist in the `LibraryDB` database.

- It throws an error if the `students` table already exists in the `LibraryDB` database.


/// type=SS, answer=[1]

In `Student.php`, what does `$sql` do on line 6?

- It holds the SQL statement.

- It executes the SQL statement. 

- It holds the `PDOStatement` object.

- It connects to the PostgreSQL database.

- It stores the variables of the DSN parameters.


/// type=MS, answer=[2,3,4,5]

In `Student.php`, which statements correctly describe `$stmt = $conn->query($sql);` on line 8?

- It connects to the PostgreSQL database.

- It calls the `query()` method of the `$conn` object.

- It returns the result set as a `PDOStatement` object.

- It executes the argument `$sql` in the `query()` method.

- It assigns the `PDOStatement` object to the variable `$stmt`.


/// type=SS, answer=[3]

In `Student.php`, what does `$stmt` do on line 8?

- It holds the SQL statement.

- It executes the SQL statement. 

- It holds the `PDOStatement` object.

- It connects to the PostgreSQL database.

- It carries the variables of the DSN parameters.


/// type=SS, answer=[5]

What does the `if` construct do on line 9 of `Student.php`?

- It adds the value of `$stmt`.

- It displays the value of `$stmt`.

- It removes the value of `$stmt`.

- It assigns a value to the `$stmt` variable.

- It evaluates the negated value of `$stmt` inside the parentheses `()`.


/// type=SS, answer=[3]

Which statement best describes the code on lines 9, 10, and 11 of `Student.php`?

- The statement displays the values assigned to the `$stmt` variable.

- The `if` statement evaluates to `true` and the statement on line 10 is executed.

- The `if` statement evaluates to `false` and the statement on line 10 is not executed.

- The `if` statement evaluates to `true` and it displays the string `Unable to create a table.`.

- The `if` statement evaluates to `false` and it displays the string `Successfully created a table.`.


/// type=SS, answer=[2]

What is the name of the table created?

- `Admin01`

- `students`

- `codestop`

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

Which statement best describes the code on lines 13, 14, and 15 of `Student.php`?

- It creates a new `Exception` class.

- It updates the `Exception` message thrown.

- It adds an exception in the statement `echo $e->getMessage()`.

- It removes an exception using the statement `echo $e->getMessage();`.

- It executes the `echo` statement if an exception occurs within the `try` block.

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
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


/// type=MS, answer=[3,4,5]

Which statements correctly describe the code on line 13 of `Connection.php`?

- It sets the values to return.

- It passes the values as an argument.

- It returns the result set as a `PDOStatement` object.

- It creates the object as an instance of the `PDO` class.

- It contains the DSN parameters to establish a connection to the PostgreSQL database.


/// type=MS, answer=[1,2,3,5], init=[commands/DataObjects/InsertJohnSmith.sql]

What values are inserted by the statement `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')` on line 6 of `Student.php`?

- `Male`

- `John`

- `Smith`

- `first_name`

- `1999-02-10`


/// type=SS, answer=[5]

In `Student.php`, what does the query `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')` do on line 6?

- It modifies multiple tables.

- It adds three columns in the `students` table.

- It inserts one column into the `students` table.

- It modifies the values `John`, `Smith`, `1999-02-10`, and `Male` in the `students` table.

- It adds a new row that contains the values `John`, `Smith`, `1999-02-10`, and `Male` in the `students` table.


/// type=MS, answer=[2,3,4,5]

Which statements correctly describe the code on line 6 of `Student.php`?

- It connects to the PostgreSQL database.

- It calls the `query()` method of the `$conn` object.

- It returns the result set as a `PDOStatement` object.

- It assigns the `PDOStatement` object to the variable `$stmt`.

- It executes the argument `INSERT INTO students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')` in the `query()` method.

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
            }
            catch (Exception $e) {
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
    $stmt = $conn->query("SELECT * FROM students");
    foreach ($stmt as $row) {
        echo $row['student_id'] . "\t";
        echo $row['first_name'] . " ";
        echo $row['last_name'] . "\t";
        echo $row['birth_date'] . "\t";
        echo $row['gender'] . "\n";
    }
?>
```
/// type=SS, answer=[5]

Execute the program. What is its output?

- It produces an error.

- No output is displayed.

- It prints `Unable to establish a connection.`.

- It prints `Successfully connected to the database.` and `John Smith 1999-10-02 Male` in separate lines.

- It prints `Successfully connected to the database.` and `1 John Smith 1999-02-10 Male` in separate lines.


/// type=SS, answer=[1]

Which value represents the `student_id` in the output `1 John Smith 1999-02-10 Male`?

- `1`

- `John`

- `Male`

- `Smith`

- `1999-02-10`


/// type=MS, answer=[3,5]

Which statements correctly describe the `foreach` construct on line 6 of `Student.php`?

- It removes all the elements in `$stmt`.

- It accesses all the elements in `$stmt`.

- It iterates through each element in the array.

- It removes all the elements in the multidimensional array `$stmt`.

- It assigns the value of the current element on each iteration to `$row`.


/// type=MS, answer=[3,4,5]

Which statements correctly describe `$stmt = $conn->query("SELECT * FROM students");` on line 5 of `Student.php`?

- It assigns the value of `$conn` to `$stmt`.

- It ends the execution of the `query()` method. 

- It calls the `query()` method of the `$conn` object.

- It assigns the result set as a `PDOStatement` object to the variable `$stmt`.

- It executes the argument `SELECT * FROM students` in the `query()` method.


/// type=SS, answer=[4]

In `Student.php`, which statement best describes `echo $row['student_id']` on line 7?

- It assigns the value `student_id` to `$row`.

- It duplicates the value with the key `student_id`.

- It returns the value with the key `student_id` from `$row`.

- It displays the value with the key `student_id` from `$row`.

- It accesses the value `student_id` from the `students` table.


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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");
    
    try {
        $conn = Connection::getConnection();
        $stmt = $conn->query("UPDATE students SET birth_date = '1990-12-24' WHERE first_name = 'John' AND last_name = 'Smith'");
        if (!$stmt) {
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


/// type=SS, answer=[4], init=[commands/DataObjects/UpdateBirthDate.sql]

In `Student.php`, which variable holds the result set as a `PDOStatement` object of the `query()` method?

- `$e`

- `$db`

- `$dsn`

- `$stmt`

- `$conn`


/// type=SS, answer=[5]

Which column is updated by the query on line 6 of `Student.php`?

- `gender`

- `student`

- `last_name`

- `first_name`

- `birth_date`


/// type=MS, answer=[2,5]

In `Student.php`, what does the `query()` method do on line 6?

- It returns the boolean value `true`.

- It returns the result set as a `PDOStatement` object.

- It holds the value of SQL statment `UPDATE students SET birth_date = '1990-12-24' WHERE first_name = 'John' AND last_name = 'Smith'`.

- It updates the prepared statement `UPDATE students SET birth_date = '1990-12-24' WHERE first_name = 'John' AND last_name = 'Smith'`.

- It executes the SQL statement `UPDATE students SET birth_date = '1990-12-24' WHERE first_name = 'John' AND last_name = 'Smith'` in a single function call.

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");
    
    try {
        $conn = Connection::getConnection();
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

- syntax error, unexpected `=` on line 6

- syntax error, unexpected `if` (T_IF) on line 7

- syntax error, unexpected `TABLE` (T_STRING) on line 6

- syntax error, unexpected `:`, expecting `,` or `)` on line 6

- syntax error, unexpected `TABLE` (T_STRING), expecting `,` or `)` on line 6


/// type=MS, answer=[3,4]

Which statements correctly describe the error?

- There is no column name specified before `VARCHAR(80)` on line 6.

- In `Student.php`, there is no comma `,` at the end of the statement on line 5.

- In `Student.php`, the SQL statement is not enclosed in double quotes `""` on line 6.

- On line 6, the statement `$stmt = $conn->query(CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10)));` is incorrect.

- There are no parentheses `()` that enclosed the statement `CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))`.

:::


/// type=CR, answer=[tests/DataObjects/MissingDoubleQuotesTest.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully created a table.`.

```php
<?php
    class Connection
    {
        const HOST = 'localhost';
        const DB = 'LibraryDB';
        const PORT = '5432';
        const USERNAME = 'codestop';
        const PASSWORD = 'Admin01';
    
        public static function getConnection() {
            try {
                return new PDO("pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD);
                
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");
    
    try {
        $conn = Connection::getConnection();
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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";
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


/// type=MS, answer=[2,5]

Which statements correctly describe the error?

- The argument passed is `$sql` on line 7.

- On line 7, the statement `$stmt = query($sql);` is incorrect.

- There are no parentheses `()` that enclosed the SQL statement on line 4.

- In `Student.php`, the semicolon `;` and the close parenthesis `)` are misplaced on line 7. 

- In `Student.php`, there are no `$conn` object and object operator `->` before `query($sql)` on line 7. 

:::


/// type=CR, answer=[tests/DataObjects/MissingObjectAndOperatorTest.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully created a table.`.

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "CREATE TABLE IF NOT EXISTS students (PRIMARY KEY (student_id), student_id INT GENERATED ALWAYS AS IDENTITY, first_name VARCHAR(80), last_name VARCHAR(80), birth_date DATE, gender VARCHAR(10))";
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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
     try {
        $conn = Connection::getConnection();
        $stmt = $conn->query("UPDATE students SET birth_date = '1990-02-10' WHERE birth_date = '1990-12-24' AND first_name = 'John'");
        if (!$stmt) {
            throw new Exception("Unable to update values in the table.");
        }
        echo "Successfully updated values in the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```
/// type=MS, answer=[1,5]

Execute the program. What are the error messages?

- Undefined variable: `conn` on line 3

- syntax error, unexpected `)` on line 3

- Uncaught Error: Call to undefined function `query()` on line 3

- syntax error, unexpected `}`, expecting the end of file on line 5

- Uncaught Error: Call to a member function `query()` on null thrown on line 3


/// type=SS, answer=[4]

Which statement best describes the error?

- In `Student.php`, there is no semicolon `;` at the end of the statement on line 3.

- In `Student.php`, the semicolon `;` and close parenthesis `)` are misplaced on line 3.

- On line 3, the values `1990-02-10`, `1990-12-24`, and `John` are enclosed in single quotes `''`.

- In `Student.php`, there is no `require_once()` statement to have the `Connection.php` file included.

- On line 3, the SQL statement `UPDATE students SET birth_date = '1990-02-10' WHERE birth_date = '1990-12-24' AND first_name = 'John'` is incorrect.

:::


/// type=CR, answer=[tests/DataObjects/MissingRequireOnceStatement.php], filename=[Connection.php,Student.php]

Correct the code so that it updates a record in the `birth_date` column with the value `1990-02-10` and displays the strings `Successfully connected to the database.` and `Successfully updated values in the table.`.

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
     try {
        $conn = Connection::getConnection();
        $stmt = $conn->query("UPDATE students SET birth_date = '1990-02-10' WHERE birth_date = '1990-12-24' AND first_name = 'John'");
        if (!$stmt) {
            throw new Exception("Unable to update values in the table.");
        }
        echo "Successfully updated values in the table.";
    } catch (Exception $e) {
        echo $e->getMessage();
    }
?>
```


:::

/// type=REPL, readonly=true, init=[commands/DataObjects/UpdateBirthDateJohnSmith.sql], filename=[Connection.php,Student.php]

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "INSERT students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')";
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

- On line 6, the `students` table does not exist.

- The `INSERT INTO` statement is miswritten as `INSERT` on line 6.

- There is no comma `,` between the values `John` and `Smith` on line 6.

- On line 6, the table named `students` is not allowed in an `INSERT` statement.

- On line 6, the SQL statement `INSERT students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')` is incorrect.

:::


/// type=CR, answer=[tests/DataObjects/InvalidSQLStatementTest.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs the strings `Successfully connected to the database.` and `Successfully inserted the values into the table.`.

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "INSERT students (first_name, last_name, birth_date, gender) VALUES ('John', 'Smith', '1999-02-10', 'Male')";
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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "INSERT INTO students (first_name, last_name, birth_date, gender)";
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

- On line 6, the `students` table does not exist.

- There are no parentheses `()` that enclosed the SQL statement on line 6.

- On line 6, the column names `first_name`, `last_name`, `birth_date`, and `gender` are not enclosed in single quotes `''`.

- In `Student.php`, there is no `VALUES` clause that specifies the values to be inserted into the selected columns on line 6.

- On line 6, the statement `$sql = "INSERT INTO students (first_name, last_name, birth_date, gender)";` is incorrect.

:::

/// type=CR, answer=[tests/DataObjects/MissingValuesClause.php], filename=[Connection.php,Student.php]

Correct the code so that it inserts the values `Samantha`, `Danes`, `1999-10-12`, and `Female` into the `students` table and displays the strings `Successfully connected to the database.` and `Successfully inserted the values into the table.`. 

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
            }
            catch (Exception $e) {
                throw new Exception("Unable to establish a connection."); 
            }
        }
    }
?>
```

```php
<?php
    require_once("./Connection.php");

    try {
        $conn = Connection::getConnection();
        $sql = "INSERT INTO students (first_name, last_name, birth_date, gender)";
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

/// type=REPL, init=[commands/DataObjects/InsertSamanthaDanes.sql], filename=[Connection.php,Student.php]

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
            }
            catch (Exception $e) {
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
    $stmt = $conn->query("SELECT * FROM students");
    foreach ($stmt as $row) {
        echo $row['student_id'] . "\t";
        echo $row['first_name'] . " ";
        echo $row['last_name'] . "\t";
        echo $row['birth_date'] . "\t";
        echo $row['gender'] . "\n";
    }
?>
```
/// type=MS, answer=[2,4]

Execute the program. What are printed on lines 2 and 3?

- No output is displayed.

- `1 John Smith 1999-02-10 Male`

- `Unable to establish a connection.`

- `2 Samantha Danes 1999-10-12 Female`

- `Successfully connected to the database.`


/// type=SS, answer=[2]

In `Student.php`, remove `as $row` in the `foreach` construct on line 6. Execute the program. What is the error message?

- Undefined variable: `row` on line 6

- syntax error, unexpected `)` on line 6

- syntax error, unexpected `foreach` on line 6

- Invalid argument supplied for `foreach()` on line 6 

- syntax error, unexpected `}`, expecting the end of file on line 6


/// type=SS, answer=[5]

Which statement best describes the error?

- The `students` table is miswritten as `student` on line 5.

- On line 6, the argument `$stmt` in the `foreach` construct is invalid.

- The name of the database is not included in the `SELECT` statement on line 5.

- In `Student.php`, there is no open curly brace `{` after `foreach ($stmt as $row)` on line 6.

- In `Student.php`, the value of the current element on each iteration is not assigned to a variable on line 6.

:::


/// type=CR, answer=[tests/DataObjects/IncorrectForeachStatement.php], filename=[Connection.php,Student.php]

Correct the code so that it outputs `Successfully connected to the database.`, `1 John Smith 1999-02-10 Male`, and `2 Samantha Danes 1999-10-12 Female` in separate lines.

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
            }
            catch (Exception $e) {
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
    $stmt = $conn->query("SELECT * FROM students");
    foreach ($stmt as $row) {
        echo $row['student_id'] . "\t";
        echo $row['first_name'] . " ";
        echo $row['last_name'] . "\t";
        echo $row['birth_date'] . "\t";
        echo $row['gender'] . "\n";
    }
?>
```

+++


+++

### Part 4: Practice

/// type=CR, answer=[tests/DataObjects/CreatePHPProgramUsingQueryMethodTest.php], init=[commands/DataObjects/UpdateStudentsTable.sql], filename=[Connection.php,Student.php]

Write a program that uses two PHP files named `Connection.php` and `Student.php` to update a value in the `students` table. First, write a PHP class named `Connection.php` that uses the `PDO_PGSQL` driver, `PDO_PGSQL DSN`, and `PDO` class to connect to the PostgreSQL database. Create the constant variables `HOST`, `DB`, `PORT`, `USERNAME`, and `PASSWORD`. Assign the values `localhost`, `LibraryDB`, `5432`, `codestop`, and `Admin01` to the constant variables respectively. Then, add a static method named `getConnection()` with `public` visibility. Inside the static method add the `try` and `catch` statements. Inside the `try` block, add a statement that returns an instance of the `PDO` class that passes the argument `"pgsql:host=" . self::HOST . ";port=". self::PORT . ";dbname=" . self::DB . ";user=" . self::USERNAME . ";password=" . self::PASSWORD`. Inside the `catch` block, throw a new exception and display the error message `Unable to establish a connection.` if an exception occurs within the `try` block.

Next, write a PHP file named `Student.php`. First, add the `require_once()` statement to have the `Connection.php` file included. Next, add a statement that assigns the call to the static method `getConnection()` of the `Connection` class to the `$conn` variable. Then, add a statement that assigns the SQL statement `UPDATE students SET gender = 'M' where gender = 'Male'` to the `$sql` variable. Add the `try` and `catch` statements. Inside the `try` block, add a statement that assigns the `query()` method call of the `$conn` object which passes the argument `$sql` to the `$stmt` variable. Then, add the `if` statement that evaluates the negated value of `$stmt` inside the parentheses `()`. Inside the `if` block, add a statement that throws an exception message `Unable to update values in the table.`. After the `if` block, add the `echo` statement that displays the string `Successfully updated values in the table.`. Inside the `catch` block, add the statement `echo $e->getMessage();`. Run the program to view the output.

```php
<?php



?>
```

```php
<?php



?>
```

+++