# mysql cheat sheet

## login from terminal:

```
sudo mysql -u root -p
```

## Show Users:

```
select * from mysql. user;
```

## Create Users:

```
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

## Grant Privileges:

```
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
```
*note that this grants root level permissions

### Here is a short list of other common possible permissions that users can enjoy.

```
    ALL PRIVILEGES- as we saw previously, this would allow a MySQL user full access to a designated database (or if no database is selected, global access across the system)
    
    CREATE- allows them to create new tables or databases
    
    DROP- allows them to them to delete tables or databases
    
    DELETE- allows them to delete rows from tables
    
    INSERT- allows them to insert rows into tables
    
    SELECT- allows them to use the SELECT command to read through databases
    
    UPDATE- allow them to update table rows
    
    GRANT OPTION- allows them to grant or remove other users’ privileges
```

To provide a specific user with a permission, you can use this framework:

```
GRANT type_of_permission ON database_name.table_name TO ‘username’@'localhost’;
```

If you want to give them access to any database or to any table, make sure to put an asterisk (*) in the place of the database name or table name.

## Revoke Privileges with:

```
REVOKE type_of_permission ON database_name.table_name FROM ‘username’@‘localhost’;

```

## Show Privileges

```
DROP USER 'username'@'localhost';
```

## Revoke Privileges with:

```
REVOKE type_of_permission ON database_name.table_name FROM ‘username’@‘localhost’;

```
Once finished with setting permissions always FLUSH privileges before exiting:

```
FLUSH PRIVILEGES;
```


##  Create Database

```
CREATE DATABASE mynewdatabase;
```

## Show Databases

```
SHOW DATABASES;
```

## Select Database for use:

```
USE mynewdatabase;
```

## Delete Database:

```
DROP DATABASE deleteMyDB
```

## Show Tables:

```
SHOW TABLES;
```

## Create Table with columns:

```
CREATE TABLE pet (
        name VARCHAR(20),
        owner VARCHAR(20),
       species VARCHAR(20), 
       sex CHAR(1), 
       birth DATE, 
       death DATE
       );
```

### Most common Data Types:

```
Data Type       Description
                   
INT	            Stores numeric values in the range of -2147483648 to 2147483647

DECIMAL	        Stores decimal values with exact precision.

CHAR	        Stores fixed-length strings with a maximum size of 255 characters.

VARCHAR	        Stores variable-length strings with a maximum size of 65,535 characters.

TEXT	        Stores strings with a maximum size of 65,535 characters.

DATE   	        Stores date values in the YYYY-MM-DD format.

DATETIME	    Stores combined date/time values in the YYYY-MM-DD HH:MM:SS format.

TIMESTAMP	    Stores timestamp values. TIMESTAMP values are stored as the number of seconds                     since the Unix epoch ('1970-01-01 00:00:01' UTC).
```


## Verify Your Created Table with:

```
DESCRIBE pet;
```


## Delete Tables:

```
DROP TABLE tablename;
```


 When supplying the data values to be inserted into the new table, the following should be considered while dealing with different data types.

* String data types - all the string values should be enclosed in single quotes.

* Numeric data types - all numeric values should be supplied directly without enclosing them   in single or double quotes. Note: numeric values like 0456 will treat the '0' as non important and it will be dropped. To avoid this wrap it with quotes like '0456'.

* Date data types - enclose date values in single quotes in the format 'YYYY-MM-DD'.

*Note - If we are supplying values for ALL the columns in the table, then we can omit the columns from the insert query.


## Insert Commands

The INSERT command creates a new row in the table to store data. 

```
single:

INSERT INTO `tablename`(column_Num) 
VALUES (Val_1);

multiple:

INSERT INTO `table_name`(column_1,column_2,...)
     VALUES (value_1,value_2,...);
```
 
## Inserting into a Table from another Table

```
INSERT INTO table_1 SELECT * FROM table_2;
```

Let's now insert all the rows from the categories table into the categories archive table.  NOTE the table structure will have to be the same for the script to work.

```
INSERT INTO `categories_archive` SELECT * FROM `categories`;
```

A more robust script is one that maps the column names in the insert table to the ones in the table containing the data. 

```
INSERT INTO `categories_archive`(category_id,category_name,remarks)  SELECT category_id,category_name,remarks FROM `categories`;
```


## Select Statement

`SELECT` is used to retrieve rows selected from one or more tables, and can include `UNION` statements and subqueries. 

The most commonly used clauses of `SELECT` statements are these:

* Each select_expr indicates a column that you want to retrieve. There must be at least one select_expr.

* table_references indicates the table or tables from which to retrieve rows. 

### SQL SELECT statement syntax

It is the most frequently used SQL command and has the following general syntax

```
SELECT [DISTINCT|ALL ] { * | [fieldExpression [AS newName]} FROM tableName [alias] [WHERE condition][GROUP BY fieldName(s)]  [HAVING condition] ORDER BY fieldName(s)
```

HERE

* `SELECT` is the SQL keyword that lets the database know that you want to retrieve data.

* `[DISTINCT | ALL]` are optional keywords that can be used to fine tune the results returnedfrom the SQL SELECT statement. If nothing is specified then ALL is assumed as the default.

* `{*| [fieldExpression [AS newName]}` at least one part must be specified, "*" selected all the fields from the specified table name, fieldExpression performs some computations on the specified fields such as adding numbers or putting together two string fields into one.

* `FROM` tableName is mandatory and must contain at least one table, multiple tables must beseparated using commas or joined using the JOIN keyword.

* `WHERE` condition is optional, it can be used to specify criteria in the result set returned from the query.

* `GROUP` BY is used to put together records that have the same field values.

* `HAVING` condition is used to specify criteria when working using the GROUP BY keyword.

* `ORDER BY` is used to specify the sort order of the result set.

### This Grabs specific columns from table:

```
SELECT `full_names`,`gender`,`physical_address`, `email`
FROM `members`;
```

### This Grabs all from table:
```
SELECT *
FROM `members`;
```

## Select with the WHERE Clause
```
SELECT Name 
FROM city 
WHERE Name LIKE 'Kal%';
```

## Select with the WHERE Clause using a range
```
SELECT * 
FROM city  
WHERE Population BETWEEN 670000 AND 700000;
```

##  Delete command syntax

The basic syntax of the delete command is as shown below. 

```
DELETE FROM `table_name` 
[WHERE condition];

DELETE FROM `movies` 
WHERE `movie_id` = 18;
```

HERE

* `DELETE FROM` table_name tells MySQL server to remove rows from the table ..

* `[WHERE condition]` is optional and is used to put a filter that restricts the number of rows 
affected by the DELETE query.

If the `WHERE` clause is not used in the `DELETE` query, then all the rows in a given table will be deleted.


## Update command syntax

 The basic syntax of the SQL Update command is as shown below.

```
UPDATE table_name SET column_name = new_value [WHERE condition];
```

 HERE

* `UPDATE` table_name is the command that tells MySQL to update the data in a table .

* `SET` column_name = new_value are the names and values of the fields to be affected by the update query. Note, when setting the update values, strings data types must be in single quotes. Numeric values do not need to be in quotation marks. Date data type must be in single quotes and in the format 'YYYY-MM-DD'.

* [`WHERE` condition]  is optional and can be used to put a filter that restricts the number of rows affected by the UPDATE query.

```
UPDATE members 
SET contact_number = '0759 253 542' 
WHERE membership_number = 1;
```

## Add in new column

If user has limited privileges, this_user needs the `ALTER` command privilege in order to change or modify the 'example' table.

That privilege is granted with the below command:

```
GRANT ALTER ON friends.* TO 'this_user'@'localhost';
```

To add a new column to an existing table, you use the `ALTER TABLE ADD COLUMN` statement as follows:

```
ALTER TABLE table
ADD [COLUMN] column_name column_definition [FIRST|AFTER existing_column];

```
## Alter a Column:

Change the `people` column name to `Peoples` with the following:

```
ALTER TABLE friends CHANGE people Peoples VARCHAR(30);
```

To add two or more columns to a table at the same time, you use the following syntax:

```
ALTER TABLE table
ADD [COLUMN] column_name_1 column_1_definition [FIRST|AFTER existing_column],
ADD [COLUMN] column_name_2 column_2_definition [FIRST|AFTER existing_column],
...;
```

```
Examples:

CREATE TABLE IF NOT EXISTS vendors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255)
);

ALTER TABLE vendors
ADD COLUMN phone VARCHAR(15) AFTER name;

INSERT INTO vendors(name,phone,vendor_group)
VALUES('IBM','(408)-298-2987',1);
 
INSERT INTO vendors(name,phone,vendor_group)
VALUES('Microsoft','(408)-298-2988',1);
```

## Distinct

### Syntax
The DISTINCT clause is used to remove duplicate rows from the result set:

```
SELECT DISTINCT column_list 
FROM table_name;
```

Here, column_list is a comma separated list of column or field names of a database table (e.g. name, age, country, etc.) whose values you want to fetch.

Note: The DISTINCT clause behaves similar to the UNIQUE constraint, except in the way it treats nulls. Two NULL values are considered unique, while at the same time they are not considered distinct from each other.


## Order By:

### Syntax

The `ORDER BY` clause is used to sort the data returned by a query in ascending or descending order. The basic syntax of this clause can be given with:

```
SELECT column_list 
FROM table_name 
ORDER BY column_name ASC|DESC;
```

Here, column_list are the names of columns/fields like name, age, country etc. of a database table whose values you want to fetch, whereas the column_name is name of the column you want to sort.


## Concantinate Columns

`Concat()` concatenates strings, appending them to each other to create one bigger string. Concat() requires one or more values to be specified, each separated by commas.

```
SELECT Concat(vend_name, ' (', vend_country, ')')
FROM vendors
ORDER BY vend_name;

output:
+--------------------------------------------+
| Concat(vend_name, ' (', vend_country, ')') |
+--------------------------------------------+
| ACME (USA)                                 |
| Anvils R Us (USA)                          |
| Furball Inc. (USA)                         |
| Jet Set (England)                          |
| Jouets Et Ours (France)                    |
| LT Supplies (USA)                          |
+--------------------------------------------+
```

The previous SELECT statements concatenate four elements:

* The name stored in the vend_name column

* A string containing a space and an open parenthesis

* The state stored in the vend_country column

* A string containing the close parenthesis

## SELECT DISTINCT Statment

* SELECT DISTINCT returns only distinct (different) values.
* SELECT DISTINCT eliminates duplicate records from the results.
* DISTINCT can be used with aggregates: COUNT, AVG, MAX, etc.
* DISTINCT operates on a single column. DISTINCT for multiple columns is not supported.

### The general syntax is:
```
SELECT DISTINCT column-name
  FROM table-name
```

Can be used with COUNT and other aggregates
```
SELECT COUNT (DISTINCT column-name)
  FROM table-name
```

## LIKE Operator
The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the LIKE operator:

`%` - The percent sign represents zero, one, or multiple characters

`_` - The underscore represents a single character

### LIKE Syntax

```
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```

```
LIKE Operator	                Description

WHERE CustomerName LIKE 'a%'	Finds any values that start with "a"
WHERE CustomerName LIKE '%a'	Finds any values that end with "a"
WHERE CustomerName LIKE '%or%'	Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%'	Finds any values that have "r" in the second position
WHERE CustomerName LIKE 'a__%'	Finds any values that start with "a" and are at least 3 characters in length
WHERE ContactName LIKE 'a%o'    Finds any values that start with "a" and ends with "o"
```

The following SQL statement selects all customers with a CustomerName starting with "a":

```
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```

The following SQL statement selects all customers with a CustomerName ending with "a":

```
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
```
The following SQL statement selects all customers with a CustomerName that have "or" in any position:

```
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```

The following SQL statement selects all customers with a CustomerName that have "r" in the second position:

```
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';
```

The following SQL statement selects all customers with a CustomerName that starts with "a" and are at least 3 characters in length:

```
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
```

The following SQL statement selects all customers with a ContactName that starts with "a" and ends with "o":

```
SELECT * FROM Customers
WHERE ContactName LIKE 'a%o';
```
The following SQL statement selects all customers with a CustomerName that does NOT start with "a":

```
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'a%';
```

## IN() function

MySQL IN() function finds a match in the given arguments.

The function returns 1 if expr is equal to any of the values in the IN list, otherwise, returns 0. If all values are constants, they are evaluated according to the type of expr and sorted. The search for the item then is done using a binary search. This means IN is very quick if the IN value list consists entirely of constants. Otherwise, type conversion takes place according to the rules.

### Syntax:
`expr IN (value,...)`

The following MySQL statement will return 1 because the specified value is within the range of values.
```
SELECT 10 IN(15,10,25);

Sample Output:

SELECT 10 IN(15,10,25);
+-----------------+
| 10 IN(15,10,25) |
+-----------------+
|               1 | 
+-----------------+
1 row in set (0.00 sec)
```
Example : IN() function with where clause

The following MySQL statement checks which books have either 300 or 400 or 500 pages.

```
SELECT book_name,dt_of_pub,no_page
FROM book_mast          
WHERE no_page IN (300,400,500);

Sample Output:

SELECT book_name,dt_of_pub,no_page
    -> FROM book_mast          
    -> WHERE no_page IN (300,400,500);
+-------------------------------------+------------+---------+
| book_name                           | dt_of_pub  | no_page |
+-------------------------------------+------------+---------+
| Understanding of Steel Construction | 2003-07-15 |     300 | 
| Fundamentals of Thermodynamics      | 2002-10-14 |     400 | 
+-------------------------------------+------------+---------+
2 rows in set (0.09 sec)
```

## CREATE INDEX

A database index is a data structure that improves the speed of operations in a table. Indexes can be created using one or more columns, providing the basis for both rapid random lookups and efficient ordering of access to records.

In MySQL, an index can be created on a table when the table is created with `CREATE TABLE` command. Otherwise, `CREATE INDEX` enables to add indexes to existing tables. A multiple-column index can be created using multiple columns.

The indexes are formed by concatenating the values of the given columns.

CREATE INDEX cannot be used to create a PRIMARY KEY.

### Syntax:

The syntax to create an index using the CREATE TABLE statement in MySQL is:

```
CREATE TABLE table_name
( 
  column1 datatype [ NULL | NOT NULL ],
  column2 datatype [ NULL | NOT NULL ],
  ...
  column_n datatype [ NULL | NOT NULL ],

  INDEX index_name [ USING BTREE | HASH ]
    (index_col1 [(length)] [ASC | DESC], 
     index_col2 [(length)] [ASC | DESC],
     ...
     index_col_n [(length)] [ASC | DESC])
);
```

OR

The syntax to create an index using the CREATE INDEX statement in MySQL is:

```
CREATE [UNIQUE | FULLTEXT | SPATIAL] INDEX index_name
  [ USING BTREE | HASH ]
  ON table_name
    (index_col1 [(length)] [ASC | DESC], 
     index_col2 [(length)] [ASC | DESC],
     ...
     index_col_n [(length)] [ASC | DESC]);
```

* **UNIQUE** - Optional. The UNIQUE modifier indicates that the combination of values in the indexed columns must be unique.

* **FULLTEXT** - Optional. The FULLTEXT modifier indexes the entire column and does not allow prefixing. InnoDB and MyISAM tables support this option.

* **SPATIAL** - Optional. The SPATIAL modifier indexes the entire column and does not allow indexed columns to contain NULL values. InnoDB (starting in MySQL 5.7) and MyISAM tables support this option.

* **index_name** - The name to assign to the index.

* **table_name** - The name of the table in which to create the index.
index_col1, index_col2, ... index_col_n
The columns to use in the index.

* **length** - Optional. If specified, only a prefix of the column is indexed not the entire column. For non-binary string columns, this value is the given number of characters of the column to index. For binary string columns, this value is the given number of bytes of the column to index.

* **ASC** - Optional. The index is sorted in ascending order for that column.

* **DESC** - Optional. The index is sorted in descending order for that column.

## Drop an Index

You can drop an index in MySQL using the `DROP INDEX` statement.

### Syntax

`DROP INDEX index_name
  ON table_name;`

* **index_name** - The name of the index to drop.

* **table_name** - The name of the table where the index was created.

## Foreign Key

A `FOREIGN KEY` is a key used to link two tables together.

A `FOREIGN KEY` is a field (or collection of fields) in one table that refers to the PRIMARY KEY in another table.

The table containing the foreign key is called the child table, and the table containing the candidate key is called the referenced or parent table.

Look at the following two tables:

"Persons" table:
```
PersonID	    LastName	    FirstName	Age
1	            Hansen	        Ola	        30
2	            Svendson	    Tove	    23
3	            Pettersen	    Kari	    20
```

"Orders" table:
```
OrderID	    OrderNumber	    PersonID
1	        77895	        3
2	        44678	        3
3	        22456	        2
4	        24562	        1
```

Notice that the "PersonID" column in the "Orders" table points to the "PersonID" column in the "Persons" table.

The "PersonID" column in the "Persons" table is the `PRIMARY KEY` in the "Persons" table.

The "PersonID" column in the "Orders" table is a `FOREIGN KEY` in the "Orders" table.

The `FOREIGN KEY` constraint is used to prevent actions that would destroy links between tables.

The `FOREIGN KEY` constraint also prevents invalid data from being inserted into the foreign key column, because it has to be one of the values contained in the table it points to.

### SQL FOREIGN KEY on CREATE TABLE

The following SQL creates a `FOREIGN KEY` on the "PersonID" column when the "Orders" table is created:

```
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
```

## DROP a FOREIGN KEY Constraint

To drop a `FOREIGN KEY` constraint, use the following SQL:

MySQL:

`ALTER TABLE Orders
DROP FOREIGN KEY FK_PersonOrder;`

## INNER JOIN

### Syntax

```
SELECT
    select_list
FROM t1
INNER JOIN t2 ON join_condition1
INNER JOIN t3 ON join_condition2
...;
```

__In this syntax:__

* First, specify the main table that appears in the FROM clause (t1).

* Second, specify the table that will be joined with the main table, which appears in the INNER JOIN clause (t2, t3,…).

* Third, specify a join condition after the ON keyword of the INNER JOIN clause. 
The join condition specifies the rule for matching rows between the main table and the table appeared in the INNER JOIN clause.

The inner join clause joins two tables based on a condition which is known as a join predicate.

The inner join clause compares each row from the first table with every row from the second table. If values in both rows cause the join condition evaluates to true, the inner join clause creates a new row whose column contains all columns of the two rows from both tables and include this new row in the final result set. In other words, the inner join clause includes only rows whose values match.

The following shows the basic syntax of the inner join clause that joins two tables table_1 and table_2:

```
SELECT column_list
FROM table_1
INNER JOIN table_2 ON join_condition;
```

If the join condition uses the equal operator (=) and the column names in both tables used for matching are the same, you can use the `USING` clause instead:

```
SELECT column_list
FROM table_1
INNER JOIN table_2 USING (column_name);
```

The following statement finds members who are also the committee members:

```
SELECT
    m.member_id,
    m.name member,
    c.committee_id,
    c.name committee
FROM
    members m
INNER JOIN committees c 
    ON c.name = m.name;
```

In this example, the inner join clause used the values in the name columns in both tables members and committees to match.

Because the name columns are the same in both tables, you can use the USING clause as shown in the following query:

```
SELECT
    m.member_id,
    m.name member,
    c.committee_id,
    c.name committee
FROM
    members m
INNER JOIN committees c USING(name);
```

## JOIN Multiple Tables

In the same way as we used `INNER JOIN` above, we simple add another INNER JOIN table reference. 

```
SELECT
    select_list
FROM t1
INNER JOIN t2 ON join_condition1
INNER JOIN t3 ON join_condition2
...;
```