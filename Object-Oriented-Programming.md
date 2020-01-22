# OBJECT-ORIENTED PROGRAMMING IN PHP

Object-Oriented Programming (PHP OOP), is a type of programming language principle added to php5, that helps in building complex, reusable web applications.

Object Oriented is an approach to software development that models application around real world objects such as employees, cars, bank accounts, etc. A class defines the properties and methods of a real world object. An object is an occurrence of a class.
The three basic components of object orientation are;

## Object Oriented Programming Principles

The three major principles of OOP are;

* **Encapsulation** – this is concerned with hiding the implementation details and only exposing the methods. The main purpose of encapsulation is to;
Reduce software development complexity – by hiding the implementation details and only exposing the operations, using a class becomes easy.
Protect the internal state of an object – access to the class variables is via methods such as get and set, this makes the class flexible and easy to maintain.
The internal implementation of the class can be changed without worrying about breaking the code that uses the class.

* **Inheritance** – this is concerned with the relationship between classes. The relationship takes the form of a parent and child. The child uses the methods defined in the parent class. The main purpose of inheritance is;
Re-usability– a number of children, can inherit from the same parent. This is very useful when we have to provide common functionality such as adding, updating and deleting data from the database.

* **Polymorphism** – this is concerned with having a single form but many different implementation ways. The main purpose of polymorphism is;
Simplify maintaining applications and making them more extendable.

## The Object Oriented concepts in PHP are:

* **Class** − This is a programmer-defined data type, which includes local functions as well as local data. You can think of a class as a template for making many instances of the same kind (or class) of object.

* **Object** − An individual instance of the data structure defined by a class. You define a class once and then make many objects that belong to it. Objects are also known as instance.

* **Inheritance** − When a class is defined by inheriting existing function of a parent class then it is called inheritance. Here child class will inherit all or few member functions and variables of a parent class.

* **Polymorphism** − This is an object oriented concept where the same function can be used for different purposes. For example: function name will remain the same but it may take different number of arguments and can do different task.

* **Overloading** − a type of polymorphism in which some or all of the operators have different implementations depending on the types of their arguments. Similarly functions can also be overloaded with different implementation.

* **Data Abstraction** − Any representation of data in which the implementation details are hidden (abstracted). * Encapsulation − refers to a concept where we encapsulate all the data and member functions together to form an object.

* **Constructor** − refers to a special type of function which will be called automatically whenever there is an object formation from a class.

* **Destructor** − refers to a special type of function which will be called automatically whenever an object is deleted or goes out of scope.


## Class & Object:

Class is a programmer-defined data type, which includes local methods and local variables. It is a collection of objects. Objects have properties and behaviors.

First we have to define a php class, where classname should be the same as filename.

Example for simple class:

```
-> is used to access an object method or property.
-> calls or sets object variables
the "this" keyword refers to the current object and is only available inside a method

<?php
class Books{
  public function name(){
  echo "Drupal book";
  }
  public function price(){
  echo "80$";
  }
}
//To create php object we have to use a `new` operator. Here the php object is the object of the Books Class.
$obj = new Books();
$obj->name();
$obj->price();
?>
```
```
Output:

Drupal book
80$
```

## Creating Objects in PHP

When a class is created, we can create any number of objects to that class. The object is created with the help of the `new` keyword.

## Calling Member Function

When the object is created we can access the variables and method function of the class with the help of operator ‘->, accessing the method is done to get the information of that method. Also look into how we can access object properties via variables

```
<?php
   class Mobile {
      /* Member variables */
      var $price;
      var $title;
      /* Member functions */
      function setPrice($par){
         $this->price = $par;
      }
      function getPrice(){
         echo $this->price ."
";
      }
      function setName($par){
         $this->title = $par;
      }
      function getName(){
         echo $this->title ."
";
      }
   }
$Samsung = new Mobile();
$Xiaomi = new Mobile();
$Iphone = new Mobile();
$Samsung->setName( "SamsungS8 );
$Iphone->setName( "Iphone7s" );
$Xiaomi->setName( "MI4" );
$Samsung->setPrice( 90000 );
$Iphone->setPrice( 65000 );
$Xiaomi->setPrice( 15000 );
Now you call another member functions to get the values set by in above example
$Samsung->getName();
$Iphone->getName();
$Xiaomi->getName();
$Samsung->getPrice();
$Iphone->getPrice();
$Xiaomi->getPrice();
?>
```
```
Output

Samsung S8
Iphone S7
MI4
90000
65000
15000
Inheritance
```

When the properties and the methods of the parent class are accessed by the child class, we call this inheritance. The child class can inherit the parent methods and can implement its own methods, this is called the overridden method. When the same method of the parent class is inherited we call this the inherited method. Now let us see types of inheritance supported in Object Oriented Programming and corresponding Php inheritance examples.

### Types Of Inheritance

```
Single Level Inheritance
Multilevel Inheritance
Single Level Inheritance:
```

In `Single Level Inheritance` the Parent class methods will be extended by the child class. All the methods can be inherited.

Example for Single Level Inheritance

```
<?php
class A {
    public function printItem($string) {
        echo 'Hi : ' . $string . "\n;
    }
    public function printPHP() {
        echo 'I am from valuebound' . PHP_EOL;
    }
}
class B extends A {
    public function printItem($string) {
        echo 'Hi: ' . $string . PHP_EOL;
    }
 public function printPHP() {
        echo "I am from ABC";
    }
}
$a = new A();
$b = new B();
$a->printItem('Raju');
$a->printPHP();       
$b->printItem('savan');
$b->printPHP();       
?>
```
```
Output

Hi : Pavan
I am from valuebound
Hi: savan
I am from ABC
```

`MultiLevel Inheritance` :

In MultiLevel Inheritance, the parent class methods will be inherited by the child class and subclass will inherit the child class methods.

```
<?php
class A {
	public function myage() {
	return  "age is 80\n";
	}
}
class B extends A {
	public function mysonage() {
	return "age is 50\n";
	}
}
class C extends B {
	public function mygrandsonage() {
	return  "age is 20\n";
	   }
        public function myHistory() {
        echo "Class A " .$this->myage();
        echo "Class B ".$this-> mysonage();
        echo "Class C " . $this->mygrandsonage();
        }
}
$obj = new C();
$obj->myHistory();
?>
```
```
Output

Class A age is 80
Class B age is 50
Class C age is 20
```