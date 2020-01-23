# PDO / MYSQLI / MYSQL

`PDO`, `MYSQL`, `MYSQL` - are PHP database extensions that are used to write PHP code for accessing the database. Once upon a time there was `mysql_` extension. It has been depricated since PHP 5.5 and removed as of PHP7. 

`MySQLI` was an improved version of `MySQL`  which provided *procedural* and *Object Oriented Programming(OOP)* support. It also added prepared statements. 

## PDO - PHP Data Objects

**PHP Data Objects(PDO)** extension is a lightweight, consistent interface for accessing databases in PHP. Each database driver that implements the PDO interface can expose database-specific features as regular extension functions. 

* You must use a database-specific PDO driver to access a database server. 

* PDO does not provide a database abstraction; it doesn't rewrite SQL or emulate missing features. 

PDO requires the new OO features in the core of PHP 5



## MySQL VS MySQLi



    MySQL	                                                                            MySQLi
    --------------------------------------------------------------------------------------------------------

    MySQL extension added in PHP version 2.0. and deprecated as of PHP 5.5.0.	        MySQLi extension added in PHP 5.5 and will work on MySQL 4.1.3 or above.            

    Does not support prepared statements.	                                            MySQLi supports prepared statements.

    MySQL provides the procedural interface.	                                        MySQLi provides both procedural and object-oriented interface.

    MySQL extension does not support stored procedure.	                                MySQLi supports store procedure.

    MySQL extension lags in security and other special features, comparatively.	        MySQLi extension is with enhanced security and improved debugging.

    Transactions are handled by SQL queries only.	                                    MySQLi supports transactions through API.

    Extension directory: ext/mysql.	                                                    Extension directory: ext/mysqli.


## PDO VS MYSQL


                                    PDO	                        MySQLi
        ---------------------------------------------------------------------------
        Database support	        12 different drivers	    MySQL only

        API	                        OOP	                        OOP + procedural

        Connection	                Easy	                    Easy

        Named parameters	        Yes	                        No

        Object mapping	            Yes                   	    Yes

        Prepared statements
        (client side)	            Yes	                        No

        Performance	                Fast	                    Fast

        Stored procedures	        Yes	                        Yes



### PDO - MySQL(PDO_MYSQL) Driver

`PDO_MYSQL` is a driver that implements the PHP Data Objects (PDO) interface to enable access from PHP to MySQL databases.

`PDO` provided an abstraction layer that allows you to use a unified API for all 12 database drivers it supports.    

Currently `PDO_MYSQL` doesnt have all of the newest and most advanced features that `MySQLi` has.



### PDO Advantages

* Useful fetch modes

* Allow to pass variables and values directly into execute

* Ability to auto-detect variable types (What actually happens is that everything is treated as a string when sent to the sever, but is converted to the correct type. This works 100% of the time with native prepared statements but doesn't work with certain edge cases, such as LIKE with emulation mode.)

* Provides an option to have automatically buffered results with prepared statements

* Named parameters (though useless with emulation mode turned off in PDO, as you can only use the same name once)


### MySQLi Advantages:

* Asynchronous queries

* Ability to get more info on affected rows, like updating a row with the same values (can be done in PDO as a constructor setting and you can't change it later)

* Proper database closing method


* Automatic cleanup with persistent connections

* MySQLi function `mysqli_query()` allows us to enforce error prone queries and prevents bugs like SQL injection.

* Using *MySQLi data fetch*, we can get *buffered* or *unbuffered* based on server resource size.

* MySQLi API allows executing multiple queries with single expression using `multi_query()` function.


## So Which Should I Use?

PDO should be used by default, especially for beginners, due to its versatility, general predictability and useful fetch modes. However, MySQLi would be a better choice for advanced users who want the newest, MySQL-specific functionality.


## Code Differences & Examples

Both `PDO` and `MySQLi` are extremely similar, but there's slight differences in syntax. MySQLi follows the old-school PHP snake_case convention, while `PDO` uses `camelCase`. Additionally, MySQLi's methods are used as object properties, while PDO uses the traditional syntax for functions.

Example of how you'd do a "non-prepared" query to fetch an associative array with MySQLi and PDO, for reference.

```
$arr = $mysqli->query("SELECT * FROM myTable")->fetch_all(MYSQLI_ASSOC);

$arr = $pdo->query("SELECT * FROM myTable")->fetchAll(PDO::FETCH_ASSOC);
```


## Creating a New Database Connection
### PDO
```
$dsn = "mysql:host=localhost;dbname=myDatabase;charset=utf8mb4";
$options = [
  PDO::ATTR_EMULATE_PREPARES   => false, // turn off emulation mode for "real" prepared statements
  PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION, //turn on errors in the form of exceptions
  PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC, //make the default fetch be an associative array
];
try {
  $pdo = new PDO($dsn, "username", "password", $options);
} catch (Exception $e) {
  error_log($e->getMessage());
  exit('Something weird happened'); //something a user can understand
}
```

### MySQLI
```
MySQLi

mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);
try {
  $mysqli = new mysqli("localhost", "username", "password", "databaseName");
  $mysqli->set_charset("utf8mb4");
} catch(Exception $e) {
  error_log($e->getMessage());
  exit('Error connecting to database'); //Should be a message a typical user could understand
}
```

## Insert, Update, Delete
### PDO

```
$stmt = $pdo->prepare("INSERT INTO myTable (name, age) VALUES (?, ?)");
$stmt->execute([$_POST['name'], 29]);
$stmt = null;
```

### MySQLi

```
$stmt = $mysqli->prepare("UPDATE myTable SET name = ? WHERE id = ?");
$stmt->bind_param("si", $_POST['name'], $_SESSION['id']);
$stmt->execute();
$stmt->close();
```

## Get Number of Affected Rows
### PDO

```
$stmt->rowCount();
```

### MySQLi

```
$stmt->affected_rows;
```

## Get Latest Primary Key Inserted

### PDO

```
$pdo->lastInsertId();
```

### MySQLi

```
$mysqli->insert_id;
```

## Get Rows Matched
### PDO

In PDO, the only way to achieve this is by setting it as a connection option to change the behavior of rowCount(), unfortunately. This means rowCount() will either return rows matched or rows changed for your entire database connection, but not both.

```
$options = [
  PDO::MYSQL_ATTR_FOUND_ROWS => true
];
```

### MySQLi

```
$mysqli->info;
```

This will output an entire string of information, like so:

```
Rows matched: 1 Changed: 0 Warnings: 0
```

I have no idea why they thought this would be a wise implementation, as it would be far more convenient in an array. Luckily, you can do this.

```
preg_match_all('/(\S[^:]+): (\d+)/', $mysqli->info, $matches); 
$infoArr = array_combine ($matches[1], $matches[2]);
var_export($infoArr);
```
Now you can access the values pretty easily. Note, that the value is a string, so you either cast all the values to ints, so === can work or strictly check with ==.

```
['Rows matched' => '1', 'Changed' => '0', 'Warnings' => '0']
```

## Fetching

Fetch Associative Array

### PDO

```
$stmt = $pdo->prepare("SELECT * FROM myTable WHERE id <= ?");
$stmt->execute([5]);
$arr = $stmt->fetchAll(PDO::FETCH_ASSOC);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$stmt = $mysqli->prepare("SELECT id, name, age FROM myTable WHERE name = ?");
$stmt->bind_param("s", $_POST['name']);
$stmt->execute();
$arr = $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

## Fetch Single Row
### PDO

```
$stmt = $pdo->prepare("SELECT id, name, age FROM myTable WHERE name = ?");
$stmt->execute([$_POST['name']]);
$arr = $stmt->fetch(PDO::FETCH_ASSOC);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$stmt = $mysqli->prepare("SELECT id, name, age FROM myTable WHERE name = ?");
$stmt->bind_param("s", $_POST['name']);
$stmt->execute();
$arr = $stmt->get_result()->fetch_assoc();
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

## Fetch Single Value (Scalar)
### PDO

```
$stmt = $pdo->prepare("SELECT id, name, age FROM myTable WHERE name = ?");
$stmt->execute([$_POST['name']]);
$arr = $stmt->fetch(PDO::FETCH_COLUMN);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$stmt = $mysqli->prepare("SELECT id, name, age FROM myTable WHERE name = ?");
$stmt->bind_param("s", $_POST['name']);
$stmt->execute();
$arr = $stmt->get_result()->fetch_row()[0];
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

## Fetch Array of Objects
### PDO

```
class myClass {}
$stmt = $pdo->prepare("SELECT name, age, weight FROM myTable WHERE name = ?");
$stmt->execute(['Joe']);
$arr = $stmt->fetchAll(PDO::FETCH_CLASS, 'myClass');
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi
```
class myClass {}
$arr = [];
$stmt = $mysqli->prepare("SELECT id, name, age FROM myTable WHERE id = ?");
$stmt->bind_param("s", $_SESSION['id']);
$stmt->execute();
$result = $stmt->get_result();
while($row = $result->fetch_object('myClass')) {
  $arr[] = $row;
}
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

`PDO` really shines here as you can see. It's very odd why MySQLi doesn't have something like `$mysqli_result->fetch_all(MYSQLI_OBJ)`. `PDO` even takes it a step further and has an awesome way to deal with the annoying default behavior of it getting called after the class constructor, via bitwising it with `fetchAll(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE, 'myClass')`. It's possible to replicate this behavior in MySQLi, but it relies on either leaving out the constructor and relying on the `magic __set()` or by only setting it in the constructor if it doesn't equal the default value.

## Like
### PDO

```
$search = "%{$_POST['search']}%";
$stmt = $pdo->prepare("SELECT id, name, age FROM myTable WHERE name LIKE ?");
$stmt->execute([$search]);
$arr = $stmt->fetchAll();
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$search = "%{$_POST['search']}%";
$stmt = $mysqli->prepare("SELECT id, name, age FROM myTable WHERE name LIKE ?"); 
$stmt->bind_param("s", $search);
$stmt->execute();
$arr = $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

## Fetch Modes

This is by far my favorite feature about PDO. The fetch modes in PDO are extremely useful and it's quite shocking that MySQLi hasn't added them yet.

## Fetch Key/Value Pair
### PDO

```
$stmt = $pdo->prepare("SELECT event_name, location FROM events WHERE id < ?");
$stmt->execute([25]);
$arr = $stmt->fetchAll(PDO::FETCH_KEY_PAIR);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$arr = [];
$id = 25;
$stmt = $con->prepare("SELECT event_name, location FROM events WHERE id < ?");
$stmt->bind_param("i", $id);
$stmt->execute();
$result = $stmt->get_result();
while($row = $result->fetch_row()) {
  $arr[$row[0]] = $row[1];
}
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

Output:

```
['Cool Event' => 'Seattle', 'Fun Event' => 'Dallas', 'Boring Event' => 'Chicago']
```

## Fetch Group Column
### PDO

```
$stmt = $pdo->prepare("SELECT hair_color, name FROM myTable WHERE id < ?");
$stmt->execute([10]);
$arr = $stmt->fetchAll(PDO::FETCH_GROUP | PDO::FETCH_COLUMN);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$arr = [];
$id = 10;
$stmt = $con->prepare("SELECT hair_color, name FROM myTable WHERE id < ?");
$stmt->bind_param("i", $id);
$stmt->execute();
$result = $stmt->get_result();
while($row = $result->fetch_row()) {
  $arr[$row[0]][] = $row[1];
}
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

Output:
```
[
  'blonde' => ['Patrick', 'Olivia'],
  'brunette' => ['Kyle', 'Ricky'],
  'red' => ['Jordan', 'Eric']
]
```

## Fetch Key/Value Pair Array
### PDO

```
$stmt = $pdo->prepare("SELECT id, max_bench, max_squat FROM myTable WHERE weight < ?");
$stmt->execute([200]);
$arr = $stmt->fetchAll(PDO::FETCH_UNIQUE);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi
```
$arr = [];
$weight = 200;
$stmt = $con->prepare("SELECT id, max_bench, max_squat FROM myTable WHERE weight < ?");
$stmt->bind_param("i", $weight);
$stmt->execute();
$result = $stmt->get_result();
$firstColName = $result->fetch_field_direct(0)->name;
while($row = $stmtResult->fetch_assoc()) {
  $firstColVal = $row[$firstColName];
  unset($row[$firstColName]);
  $arr[$firstColVal] = $row;
}
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

Output:
```
[
  17 => ['max_bench' => 230, 'max_squat' => 175],
  84 => ['max_bench' => 195, 'max_squat' => 235],
  136 => ['max_bench' => 135, 'max_squat' => 285]
]
```

## Fetch Group
### PDO

```
$stmt = $pdo->prepare("SELECT hair_color, name, age FROM myTable WHERE id < ?");
$stmt->execute([12]);
$arr = $stmt->fetchAll(PDO::FETCH_GROUP);
if(!$arr) exit('No rows');
var_export($arr);
$stmt = null;
```

### MySQLi

```
$arr = [];
$id = 12;
$stmt = $con->prepare("SELECT hair_color, name, age FROM myTable WHERE id < ?");
$stmt->bind_param("i", $id);
$stmt->execute();
$result = $stmt->get_result();
$firstColName = $result->fetch_field_direct(0)->name;
while($row = $stmtResult->fetch_assoc()) {
  $firstColVal = $row[$firstColName];
  unset($row[$firstColName]);
  $arr[$firstColVal][] = $row;
}
if(!$arr) exit('No rows');
var_export($arr);
$stmt->close();
```

Output:

```
[
  'blonde' => [
    ['name' => 'Patrick', 'age' => 22],
    ['name' => 'Olivia', 'age' => 18]
  ],
  'brunette'  => [
    ['name' => 'Kyle', 'age'=> 25],
    ['name' => 'Ricky', 'age' => 34]
  ],
   'red'  => [
    ['name' => 'Jordan', 'age' => 17],
    ['name' => 'Eric', 'age' => 52]
  ]
]
```

## Where In Array
### PDO

```
$inArr = [1, 3, 5];
$clause = implode(',', array_fill(0, count($inArr), '?')); //create 3 question marks
$stmt = $pdo->prepare("SELECT * FROM myTable WHERE id IN ($clause)");
$stmt->execute($inArr);
$resArr = $stmt->fetchAll();
if(!$resArr) exit('No rows');
var_export($resArr);
$stmt = null;
```

### MySQLi
```
$inArr = [12, 23, 44];
$clause = implode(',', array_fill(0, count($inArr), '?')); //create 3 question marks
$types = str_repeat('i', count($inArr)); //create 3 ints for bind_param
$stmt = $mysqli->prepare("SELECT id, name FROM myTable WHERE id IN ($clause)");
$stmt->bind_param($types, ...$inArr);
$stmt->execute();
$resArr = $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
if(!$resArr) exit('No rows');
var_export($resArr);
$stmt->close();
```

## Where In Array With Other Placeholders
### PDO

```
$inArr = [1, 3, 5];
$clause = implode(',', array_fill(0, count($inArr), '?')); //create 3 question marks
$stmt = $pdo->prepare("SELECT * FROM myTable WHERE id IN ($clause) AND id < ?");
$fullArr = array_merge($inArr, [5]); //merge WHERE IN array with other value(s)
$stmt->execute($fullArr);
$resArr = $stmt->fetchAll();
if(!$resArr) exit('No rows');
var_export($resArr);
$stmt = null;
```

### MySQLi

```
$inArr = [12, 23, 44];
$clause = implode(',', array_fill(0, count($inArr), '?')); //create 3 question marks
$types = str_repeat('i', count($inArr)); //create 3 ints for bind_param
$types .= 'i'; //add 1 more int type
$fullArr = array_merge($inArr, [26]); //merge WHERE IN array with other value(s)
$stmt = $mysqli->prepare("SELECT id, name FROM myTable WHERE id IN ($clause) AND age > ?");
$stmt->bind_param($types, ...$fullArr); //4 placeholders to bind
$stmt->execute();
$resArr = $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
if(!$resArr) exit('No rows');
var_export($resArr);
$stmt->close();
```

## Transactions
### PDO

```
try {
  $pdo->beginTransaction();
  $stmt1 = $pdo->prepare("INSERT INTO myTable (name, state) VALUES (?, ?)");
  $stmt2 = $pdo->prepare("UPDATE myTable SET age = ? WHERE id = ?");
  if(!$stmt1->execute(['Rick', 'NY'])) throw new Exception('Stmt 1 Failed');
  else if(!$stmt2->execute([27, 139])) throw new Exception('Stmt 2 Failed');
  $stmt1 = null;
  $stmt2 = null;
  $pdo->commit();
} catch(Exception $e) {
  $pdo->rollback();
  throw $e;
}
```

We are checking for truthiness on execute() with PDO is due to the fact that it can return false, while silently failing. Here's a more detailed explanation.

### MySQLi

```
try {
  $mysqli->autocommit(FALSE); //turn on transactions
  $stmt1 = $mysqli->prepare("INSERT INTO myTable (name, age) VALUES (?, ?)");
  $stmt2 = $mysqli->prepare("UPDATE myTable SET name = ? WHERE id = ?");
  $stmt1->bind_param("si", $_POST['name'], $_POST['age']);
  $stmt2->bind_param("si", $_POST['name'], $_SESSION['id']);
  $stmt1->execute();
  $stmt2->execute();
  $stmt1->close();
  $stmt2->close();
  $mysqli->autocommit(TRUE); //turn off transactions + commit queued queries
} catch(Exception $e) {
  $mysqli->rollback(); //remove all queries from queue if error (undo)
  throw $e;
}
```

## Named Parameters

This is a PDO-only feature, but it's only useful if emulation mode is turned off. Otherwise, you can only use the same variable once. It should also be noted that the leading colon is not required, but this isn't documented anywhere. It likely will eventually anyway, but you never know, I suppose. You also can't mix ? placeholders with named ones; it's either one or the other.

```
$stmt = $pdo->prepare("UPDATE myTable SET name = :name WHERE id = :id");
$stmt->execute([':name' => 'David', ':id' => 3]);
$stmt = null;
```