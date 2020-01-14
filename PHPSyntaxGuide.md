# Welcome to my PHP Syntax Guide

## PHP Comments

Write php comments to give your code more readability with the following:

```
# single line comment
/ single line comment
/* multi-line comment */
```

## PHP Variables

Define and Call Variables with '$'.

```
$myVariable = 'this is my new variable';
```

## PHP Echo / Print

The echo() Outputs one or more strings. Use it to print to the screen. 

It is not actually a function, so no parentheses are required. You can however pass multiple  strings through echo.

echo() is slightly faster than print.

```
<?php
echo 'This ', 'string ', 'was ', 'made ', 'with multiple parameters.'

echo 'This ' . 'string ' . 'was ' . 'made ' . 'with concatenation.' . "\n";

echo "Sum: ", 1 + 2;
?>
```

The main difference between echo and print are that print only accepts a single argument and always returns 1.

```
print("hello world);

print "print() also works without parentheses.";

print "This spans
multiple lines. The newlines will be
output as well";

// You can use variables inside a print statement
$foo = "foobar";
$bar = "barbaz";

print "foo is $foo"; // foo is foobar

// You can also use arrays
$bar = array("value" => "foo");

print "this is {$bar['value']} !"; // this is foo !;
```

## PHP Data Types
 
### PHP supports the following data types:

1. String // `$string = "Hello world!";`

2. Integer // `$integer = 1441;`

3. Float (floating point numbers - also called double) // `$float = 5.432`

4. Boolean // `$boolean = true; $boolean = false;`

5. Array // `$myArray = array('jim', 'jones', 'jimbob', 'jr');`

6. Object // A class is a template for objects, and an object is an instance of class.

Let's assume we have a class named Fruit. A Fruit can have properties like name, color, weight, etc. We can define variables like `$name`, `$color`, and `$weight` to hold the values of these properties. 

When the individual objects (apple, banana, etc.) are created, they inherit all the properties and behaviors from the class, but each object will have different values for the properties.

Below we declare a class named Fruit consisting of two properties ($name and $color) and two methods set_name() and get_name() for setting and getting the $name property:

```
<?php
class Fruit {
  // Properties
  public $name;
  public $color;

  // Methods
  function set_name($name) {
    $this->name = $name;
  }
  function get_name() {
    return $this->name;
  }
  function set_color($color) {
    $this->color = $color;
  }
  function get_color() {
    return $this->color;
  }
}

$apple = new Fruit();
$apple->set_name('Apple');
$apple->set_color('Red');
echo "Name: " . $apple->get_name();
echo "<br>";
echo "Color: " . $apple->get_color();
?>
```
__Note: In a class, variables are called properties and functions are called methods!__


7. NULL:  NULL value represents a variable with no value. `$var = NULL;`

A variable is considered to be null if:

* it has been assigned the constant NULL.

* it has not been set to any value yet.

* it has been unset().

8. Resource: is not an actual data type but it is a special variable, holding a reference to an external resource. Resources are created and used by special functions.

For example, when we attempt to access the database or a file resource, we can have a resource identifier. This identifier will be used to hook the resource to access data.

The following code shows how to get the database resource identifier by requesting the MySQL connection. In this code, the database information is specified for the mysqli_connect() and it returns MySQL connection object as a resource identifier.

`$conn = mysqli_connect(localhost,"root","admin","animals");`

## PHP Strings

useful string methods:

strlen() - Return the Length of a String

`<?php
echo strlen("Hello world!"); // outputs 12
?>`
 
str_word_count() - Count Words in a String

`<?php
echo str_word_count("Hello world!"); // outputs 2
?>`

strrev() - Reverse a String

`<?php
echo strrev("Hello world!"); // outputs !dlrow olleH
?>`

strpos() - Search For a Text Within a String

`<?php
echo strpos("Hello world!", "world"); // outputs 6
?>`

str_replace() - Replace Text Within a String

`<?php
echo str_replace("world", "Dolly", "Hello world!"); // outputs Hello Dolly!
?>
`

### The following is a list of all string functions:

```
Function	Description
addcslashes()	Returns a string with backslashes in front of the specified characters
addslashes()	Returns a string with backslashes in front of predefined characters
bin2hex()	Converts a string of ASCII characters to hexadecimal values
chop()	Removes whitespace or other characters from the right end of a string
chr()	Returns a character from a specified ASCII value
chunk_split()	Splits a string into a series of smaller parts
convert_cyr_string()	Converts a string from one Cyrillic character-set to another
convert_uudecode()	Decodes a uuencoded string
convert_uuencode()	Encodes a string using the uuencode algorithm
count_chars()	Returns information about characters used in a string
crc32()	Calculates a 32-bit CRC for a string
crypt()	One-way string hashing
echo()	Outputs one or more strings
explode()	Breaks a string into an array
fprintf()	Writes a formatted string to a specified output stream
get_html_translation_table()	Returns the translation table used by htmlspecialchars() and htmlentities()
hebrev()	Converts Hebrew text to visual text
hebrevc()	Converts Hebrew text to visual text and new lines (\n) into <br>
hex2bin()	Converts a string of hexadecimal values to ASCII characters
html_entity_decode()	Converts HTML entities to characters
htmlentities()	Converts characters to HTML entities
htmlspecialchars_decode()	Converts some predefined HTML entities to characters
htmlspecialchars()	Converts some predefined characters to HTML entities
implode()	Returns a string from the elements of an array
join()	Alias of implode()
lcfirst()	Converts the first character of a string to lowercase
levenshtein()	Returns the Levenshtein distance between two strings
localeconv()	Returns locale numeric and monetary formatting information
ltrim()	Removes whitespace or other characters from the left side of a string
md5()	Calculates the MD5 hash of a string
md5_file()	Calculates the MD5 hash of a file
metaphone()	Calculates the metaphone key of a string
money_format()	Returns a string formatted as a currency string
nl_langinfo()	Returns specific local information
nl2br()	Inserts HTML line breaks in front of each newline in a string
number_format()	Formats a number with grouped thousands
ord()	Returns the ASCII value of the first character of a string
parse_str()	Parses a query string into variables
print()	Outputs one or more strings
printf()	Outputs a formatted string
quoted_printable_decode()	Converts a quoted-printable string to an 8-bit string
quoted_printable_encode()	Converts an 8-bit string to a quoted printable string
quotemeta()	Quotes meta characters
rtrim()	Removes whitespace or other characters from the right side of a string
setlocale()	Sets locale information
sha1()	Calculates the SHA-1 hash of a string
sha1_file()	Calculates the SHA-1 hash of a file
similar_text()	Calculates the similarity between two strings
soundex()	Calculates the soundex key of a string
sprintf()	Writes a formatted string to a variable
sscanf()	Parses input from a string according to a format
str_getcsv()	Parses a CSV string into an array
str_ireplace()	Replaces some characters in a string (case-insensitive)
str_pad()	Pads a string to a new length
str_repeat()	Repeats a string a specified number of times
str_replace()	Replaces some characters in a string (case-sensitive)
str_rot13()	Performs the ROT13 encoding on a string
str_shuffle()	Randomly shuffles all characters in a string
str_split()	Splits a string into an array
str_word_count()	Count the number of words in a string
strcasecmp()	Compares two strings (case-insensitive)
strchr()	Finds the first occurrence of a string inside another string (alias of strstr())
strcmp()	Compares two strings (case-sensitive)
strcoll()	Compares two strings (locale based string comparison)
strcspn()	Returns the number of characters found in a string before any part of some specified characters are found
strip_tags()	Strips HTML and PHP tags from a string
stripcslashes()	Unquotes a string quoted with addcslashes()
stripslashes()	Unquotes a string quoted with addslashes()
stripos()	Returns the position of the first occurrence of a string inside another string (case-insensitive)
stristr()	Finds the first occurrence of a string inside another string (case-insensitive)
strlen()	Returns the length of a string
strnatcasecmp()	Compares two strings using a "natural order" algorithm (case-insensitive)
strnatcmp()	Compares two strings using a "natural order" algorithm (case-sensitive)
strncasecmp()	String comparison of the first n characters (case-insensitive)
strncmp()	String comparison of the first n characters (case-sensitive)
strpbrk()	Searches a string for any of a set of characters
strpos()	Returns the position of the first occurrence of a string inside another string (case-sensitive)
strrchr()	Finds the last occurrence of a string inside another string
strrev()	Reverses a string
strripos()	Finds the position of the last occurrence of a string inside another string (case-insensitive)
strrpos()	Finds the position of the last occurrence of a string inside another string (case-sensitive)
strspn()	Returns the number of characters found in a string that contains only characters from a specified charlist
strstr()	Finds the first occurrence of a string inside another string (case-sensitive)
strtok()	Splits a string into smaller strings
strtolower()	Converts a string to lowercase letters
strtoupper()	Converts a string to uppercase letters
strtr()	Translates certain characters in a string
substr()	Returns a part of a string
substr_compare()	Compares two strings from a specified start position (binary safe and optionally case-sensitive)
substr_count()	Counts the number of times a substring occurs in a string
substr_replace()	Replaces a part of a string with another string
trim()	Removes whitespace or other characters from both sides of a string
ucfirst()	Converts the first character of a string to uppercase
ucwords()	Converts the first character of each word in a string to uppercase
vfprintf()	Writes a formatted string to a specified output stream
vprintf()	Outputs a formatted string
vsprintf()	Writes a formatted string to a variable
wordwrap()	Wraps a string to a given number of characters
```

## PHP Numbers
 
An integer is a number without any decimal part.

An integer data type is a non-decimal number between -2147483648 and 2147483647. A value greater (or lower) than this, will be stored as float, because it exceeds the limit of an integer.

Another important thing to know is that even if 4 * 2.5 is 10, the result is stored as float, because one of the operands is a float (2.5).

Here are some rules for integers:

* An integer must have at least one digit
* An integer must not have a decimal point
* An integer can be either positive or negative

Integers can be specified in three formats: decimal (10-based), hexadecimal (16-based - prefixed with 0x) or octal (8-based - prefixed with 0)
PHP has the following functions to check if the type of a variable is integer:

```
is_int()
is_integer() - alias of is_int()
is_long() - alias of is_int()
```

## PHP Constants
 
Constants are like variables except that once they are defined they cannot be changed or undefined.

A valid constant name starts with a letter or underscore (no $ sign before the constant name).

Note: Unlike variables, constants are automatically global across the entire script.

To create a constant, use the `define()` function.

### syntax

define(name, value, case-insensitive)

Parameters:

* name: Specifies the name of the constant
* value: Specifies the value of the constant
* case-insensitive: Specifies whether the constant name should be case-insensitive. Default is false

Create a constant with a case-sensitive name:

`<?php
define("GREETING", "Welcome to W3Schools.com!");
echo GREETING;
?>`

Create a constant with a case-insensitive name:

`<?php
define("GREETING", "Welcome to W3Schools.com!", true);
echo greeting;
?>`

## PHP Operators
 
Operators are used to perform operations on variables and values.

PHP divides the operators in the following groups:

* Arithmetic operators
* Assignment operators
* Comparison operators
* Increment/Decrement operators
* Logical operators
* String operators
* Array operators
* Conditional assignment operators

### PHP Arithmetic Operators

The PHP arithmetic operators are used with numeric values to perform common arithmetical operations, such as addition, subtraction, multiplication etc.

```
Operator	Name	        Example	    Result	
+	        Addition	    $x + $y	    Sum of $x and $y	
-	        Subtraction	    $x - $y	    Difference of $x and $y	
*	        Multiplication	$x * $y	    Product of $x and $y	
/	        Division	    $x / $y	    Quotient of $x and $y	
%	        Modulus	        $x % $y	    Remainder of $x divided by $y	
**	        Exponentiation	$x ** $y	Result of raising $x to the $y'th power
```

### PHP Assignment Operators

The PHP assignment operators are used with numeric values to write a value to a variable.

```
Assignment	Same as...	    Description
x = y	    x = y	        The left operand gets set to the value of the expression on the right	
x += y	    x = x + y	    Addition	
x -= y	    x = x - y	    Subtraction	
x *= y	    x = x * y	    Multiplication	
x /= y	    x = x / y	    Division	
x %= y	    x = x % y	    Modulus
```

### PHP Comparison Operators

The PHP comparison operators are used to compare two values (number or string):

```
Operator	    Name	                    Example	    Result
==	            Equal	                    $x == $y	Returns true if $x is equal to $y	
===	            Identical	                $x === $y	Returns true if $x is equal to $y, and they are of the same type	
!=	            Not equal	                $x != $y	Returns true if $x is not equal to $y	
<>	            Not equal	                $x <> $y	Returns true if $x is not equal to $y	
!==	            Not identical	            $x !== $y	Returns true if $x is not equal to $y, or they are not of the same type	
>	            Greater than	            $x > $y	    Returns true if $x is greater than $y	
<	            Less than	                $x < $y	    Returns true if $x is less than $y	
>=	            Greater than or equal to	$x >= $y	Returns true if $x is greater than or equal to $y	
<=	            Less than or equal to	    $x <= $y	Returns true if $x is less than or equal to $y	
<=>	            Spaceship	$x <=> $y	                Returns an integer less than, equal to, or greater than zero, depending on if $x is less than,                                                           equal to, or greater than $y. Introduced in PHP 7.
```

### PHP Increment / Decrement Operators

The PHP increment operators are used to increment a variable's value.

The PHP decrement operators are used to decrement a variable's value.

```
Operator	Name	            Description
++$x	    Pre-increment	    Increments $x by one, then returns $x	
$x++	    Post-increment	    Returns $x, then increments $x by one	
--$x	    Pre-decrement	    Decrements $x by one, then returns $x	
$x--	    Post-decrement	    Returns $x, then decrements $x by one
```

### PHP Logical Operators

The PHP logical operators are used to combine conditional statements.

```
Operator	Name	        Example	        Result
and	        And	            $x and $y	    True if both $x and $y are true	
or	        Or	            $x or $y	    True if either $x or $y is true	
xor	        Xor	            $x xor $y	    True if either $x or $y is true, but not both	
&&	        And	            $x && $y	    True if both $x and $y are true	
||	        Or	            $x || $y	    True if either $x or $y is true	
!	        Not	            !$x	            True if $x is not true
```

### PHP String Operators

PHP has two operators that are specially designed for strings.

```
Operator	Name	                    Example	            Result
.	        Concatenation	            $txt1 . $txt2	    Concatenation of $txt1 and $txt2	
.=	        Concatenation assignment	$txt1 .= $txt2	    Appends $txt2 to $txt1
```

### PHP Array Operators

The PHP array operators are used to compare arrays.

```
Operator	        Name	        Example	        Result
+	                Union	        $x + $y	        Union of $x and $y	
==	                Equality	    $x == $y	    Returns true if $x and $y have the same key/value pairs	
===	                Identity	    $x === $y	    Returns true if $x and $y have the same key/value pairs in the same order and of the same types	
!=	                Inequality	    $x != $y	    Returns true if $x is not equal to $y	
<>	                Inequality	    $x <> $y	    Returns true if $x is not equal to $y	
!==	                Non-identity	$x !== $y	    Returns true if $x is not identical to $y
```

### PHP Conditional Assignment Operators

The PHP conditional assignment operators are used to set a value depending on conditions:

```
Operator	    Name	            Example	                        Result
?:	            Ternary	            $x = expr1 ? expr2 : expr3	    Returns the value of $x.
                                                                    The value of $x is expr2 if expr1 = TRUE.
                                                                    The value of $x is expr3 if expr1 = FALSE.	

??	            Null coalescing	    $x = expr1 ?? expr2	Returns     the value of $x.
                                                                    The value of $x is expr1 if expr1 exists, and is not NULL.
                                                                    If expr1 does not exist, or is NULL, the value of $x is expr2.
                                                                    Introduced in PHP 7
```


## PHP If & Else & Elseif
 
Conditional statements are used to perform different actions based on different conditions.

In PHP we have the following conditional statements:

* if statement - executes some code if one condition is true

```
if (condition) {
    code to be executed if condition is true;
}
```

* if...else statement - executes some code if a condition is true and another code if that condition is false

```
if (condition) {
    code to be executed if condition is true;
} else {
    code to be executed if condition is false;
}
```

* if...elseif...else statement - executes different codes for more than two conditions

```
if (condition) {
    code to be executed if this condition is true;
} elseif (condition) {
    code to be executed if first condition is false and this condition is true;
} else {
    code to be executed if all conditions are false;
}
```

* switch statement - selects one of many blocks of code to be executed

```
switch (n) {
    case label1:
        code to be executed if n=label1;
        break;
    case label2:
        code to be executed if n=label2;
        break;
    case label3:
        code to be executed if n=label3;
        break;
    default:
        code to be executed if n is different from all labels;
}
```

## PHP Functions

PHP has more than 1000 built-in functions, and in addition you can create your own custom functions.

Create a simple function with:

```
function functionName() {
    code to be executed;
}
```

HP automatically associates a data type to the variable, depending on its value. Since the data types are not set in a strict sense, you can do things like adding a string to an integer without causing an error.

In PHP 7, type declarations were added. This gives us an option to specify the expected data type when declaring a function, and by adding the strict declaration, it will throw a "Fatal Error" if the data type mismatch.

In the following example we try to send both a number and a string to the function without using strict:

```
<?php
function addNumbers(int $a, int $b) {
    return $a + $b;
}
echo addNumbers(5, "5 days");
// since strict is NOT enabled "5 days" is changed to int(5), and it will return 10
?>
```
To specify strict we need to set declare(strict_types=1);. This must be on the very first line of the PHP file.

In the following example we try to send both a number and a string to the function, but here we have added the strict declaration:

```
<?php declare(strict_types=1); // strict requirement

function addNumbers(int $a, int $b) {
    return $a + $b;
}
echo addNumbers(5, "5 days");
// since strict is enabled and "5 days" is not an integer, an error will be thrown
?>
```

## PHP Arrays
 
An array stores multiple values in one single variable:

```
$cars = array("Volvo", "BMW", "Toyota");
```

## PHP Loop

Loops are used to execute the same block of code again and again, as long as a certain condition is true.

`while` - loops through a block of code as long as the specified condition is true

```
while (condition is true) {
    code to be executed;
}
```

`do...while` - loops through a block of code once, and then repeats the loop as long as the specified condition is true

```
do {
    code to be executed;
} while (condition is true);
```

`for` - loops through a block of code a specified number of times

```
for ($x = 0; $x <= 10; $x++) {
    echo "The number is: $x <br>";
}
```

`foreach` - loops through a block of code for each element in an array

```
foreach ($array as $value) {
  code to be executed;
}
```