## Defining the term *class*
* Is a blueprint/recipe/template that creates objects of specific types. Objects are also called *instances* of a class
* Encapsulates data (fields/variables) and behaviour (methods) in a single unit


## Class representation
<img src=media/sample_class.png width=650 height=400 /></br>
<!-- * //TODO image from c++ book pg.241 -->


## Porting a 'logical' entity into a class
<img src=media/circle.png width=300 height=300 /></br>
* Circle's attributes:
  * x coordinate
  * y coordinate
  * radius


## Class name
```java
public class Circle {
	/* class body */
}
```
* *Public* is the access modifier of the class. *Public* makes this class visible to classes in  other packages
* **Important** 
  * Filenames should have the same name with the class ending with the *.java* extension
* Good practice: 
  * Class names should begin with a capital letter and follow the camel-case style
  * Examples: MyCustomClass, DatabaseConnection


## Instance variables
```java
class Circle {
	/* Instance variables are defined here*/
	
	/* Point x coordinate */ 
	private int x;
	/* Point y coordinate */
	private int y;
	/* Circle's radius */
	private int radius;
}
```
* Fields have a type, a name and (optionally) an access modifier
* Good practice: 
 * Instance variables' names should begin with a lower-case letter and follow the camel-case style. Example: firstName, lastName, telephoneNumber
 * Instance variables should have a private access modifier


## Class methods
```java
class Circle {

	/* Point x coordinate */ 
	private int x;
	/* Point y coordinate */
	private int y;
	/* Circle's radius */
	private int radius;

	/* Methods are defined here */

	/* Returns the x coordinate */
	public int getX() { return x; }
	/* Returns the y coordinate */
	public int getY() { return y; }
	/* Returns the radius */
	public int getRadius() { return radius; }
}
```
* Methods, have a (return) type, a name, (optionally) an access modifier and (optionally) one or more arguments/parameters 


## Access modifiers
* *public* - visible to all classes
* *private* - visible only inside the current class
* *protected* - Visible only to subclasses of the current class
<br><br>
* Good practices:
 * All fields should be *private*
 * Methods that are not design to interact with other classes should also be *private*


## Getters and setters methods
* Fields should be accessed and modified only through dedicated methods
```java
class Circle {

	/* x and y coordinates and radius */
	private int x;
	private int y; 
	private int radius;

	/* getters and setters methods */
	public void setX(int x) { this.x = x; }
	public int getX() { return this.x; }
	public void setY(int y) { this.y = y; }
	public int getY() { return this.y; }
	public void setRadius(int r) { this.radius = r; }
	public int getRadius() { return radius; }
}
```


## Getters and setters methods
* Recommended way to access or modify fields
```java
Circle c = new Circle();
c.setX(5);
c.setY(3);
System.out.println("Hello, I'm circle (" + p.getX() + "," + p.getY() + ")");
```
```java
I'm circle (5,3)
```
* And never directly (this would be possible only if *x* and *y* instance variables had public access
```java
Circle c = new Circle();
c.x = 5;
c.y = 3;
System.out.println("Hello, I'm circle (" + p.x + "," + p.y + ")");
``` 


## The keyword *this*
```java
class Circle {

	/* x and y coordinates and radius */
	private int x;
	private int y; 
	private int radius;

	public void setCoordinates(int x, int y) {
		this.x = x;
		this.y = y;
	}
}
```
* The keyword **this** refer to the instance variables
* Good practice:
 * Always use **this** when you are refering to an instance variable


## Anatomy of a method
```java
public double getPerimeter(double pi) {
	double perimeter = 2*pi*this.radius;
	return perimeter; 
}
```
* *public* : access modifier
* *double* : return type
* *getPerimeter* : name
* *pi* : argument/parameter of type double named as *pi*
<br><br>
A method's **signature** is the method name + the parameters. Signature defines how a method can be Overloaded
```java
public double getPerimeter(double pi)
```


## Non-returning methods
**void** methods perform an operation without returning a value
<br><br>
```java
public void printPerimeter(double pi) {
	double perimeter = 2*pi*this.radius;
	System.out.println("Perimeter is " + perimeter); 
}
```


## Overloading methods
Is the ability to have more than one methods with the same name **but** with different parameters. Different in sense of, type, number and order
```java
/** valid overloaded methods **/
public void dummy() {}
public void dummy(String message) {} // different number of arguments
public void dummy(String message, int number) {} // different number of arguments
public void dummy(int number) {} // different number of arguments
public void dummy(int number, String message) {} // different order of arguments
public void dummy(float number) {} // different type of arguments
public int dummy(String message, double d) { return 0; } // different return type. The return type does not affect the overloading process
private void dummy(int[] array) {} // different type of arguments. Private does not affect the overloading process
public static void dummy(double real) {} // static modifier does no affect the overlaoding process
public final void dummy(float f1, float f2) {} // final modifier does no affect the overlaoding process

/** invalid overloaded methods **/
public void dummy(String text) {} // different argument name but same type
public void dummy(String message, int x) {} // the same as above
```
In other words, only the **signature** of the method affects its overloading ability


## Constructor - a special method!
```java
/* default constructor */
Circle() {
	this.x = this.y = 0; // you can omit this line. x and will be initialized to zero either way. 
	this.radius = 3;
}
```
* Creating an object of type Circle:
```java
	Circle c = new Circle();
```
* Constructors should have the same name with the *class*
* Constructors inherit the class's access modifier


## Overloaded constructor
```java
/* Overloaded constructor */
Circle(int x, int y) {
	this.x = x;
	this.y = y;
	this.radius = 3; //hard coded
}
/* Overloaded constructor */
Circle(int x, int y, int r) {
	this.x = x;
	this.y = y;
	this.radius = r;
}
```
Creating instances of type Circle:
```java
	Circle c1 = new Circle();
	Circle c2 = new Circle(4,4);
	Circle c3 = new Circle(3,4,5);
```


## Chaining constructors
* Similarly, a constructor with the **this** call can trigger any other constructor in the class!
```java
/* default constructor */
Circle() {
	this.x = 0;
	this.y = 0;
	this.radius = 3;
}
/* Overloaded constructor calling the default 
   constructor with the use of this */
Circle(int x, int y) {
	this();
	this.x = x;
	this.y = y;
}
```
Creating instances of type Circle:
```java
	Circle c2 = new Circle(2,3);
```


## Copying objects
```java
Circle c1 = new Circle(5,2,5);
Circle c2 = new Circle(10,4,10);
c2 = c1;
```
* The perimeters of **c1** and **c2** are equal or different? 


## Memory allocation
<img src=media/memory.svg width=700 height=450 /></br>
```java
Circle c1 = new Circle(5,2,5);
Circle c2 = new Circle(10,4,10);
c2 = c1;
```


## Copying objects (2)
```java
c1.calculatePerimeter();
c2.calculatePerimeter();
```
* Results to:
```java
Perimeter is 18.84
Perimeter is 18.84
```


## Copying objects (3)
```java
Circle c1 = new Circle(5,5);
Circle c2 = c1;
c2.setRadius(10);
c1.calculatePerimeter();
c2.calculatePerimeter();
```
* Are the perimeters equal or not?


## Copying objects (4)
```java
Circle c1 = new Circle(5,5);
Circle c2 = c1;
c2.setRadius(10);
c1.calculatePerimeter();
c2.calculatePerimeter();
```
* Results to:
```java
Perimeter is 18.84
Perimeter is 18.84
```


## Copy constructor
```java
/* Regular Overloaded Constructor */
Circle(int x, int y, int r) {
	this.x = x;
	this.y = y;
	this.radius = r;
}

/* Copy Constructor */
public Circle(Circle original) {
	this(original.x, original.y, original.radius);
}
```
* Copying/cloning an object process:
 * Create a new object of type circle
 * Assign the values of the old object to the new
 * Return the new object
```java
Circle original = new Circle(5,2);
Circle copyOfOriginal = new Circle(original);
```


## Garbage Collector and Destructor method
```java
/** Circle destructor */
public void finalize() {
    System.out.println("Circle (" + 
    	this.x +"," + this.y + "," + this.radius + ") deleted");
}
```
* Release the memory and run the *garbage collector*
```java
c = null;
System.gc(); // Garbage Collector call
```
* Results to
```java
Circle (5,5,10) deleted
```
* The garbage collection is a process that identifies unused object that are no longer referenced by any part of your program and reclaims the allocated memory


## Static fields and methods
```java
class Circle {
	/* counts the number of the created circles */
	public static int count;

	/* Constructor */
	Circle() {
		count += 1; // increase count by one after creating a new circle 
	}
}
```
* *Static* fields are common for all instances of the class
```java
Circle c1 = new Circle();
Circle c2 = new Circle();
System.out.println("c1 count is " + c1.count); //c1.count gives a warning. Why?
System.out.println("c2 count is " + Circle.count);
```


## Static fields and methods (2)
```java
c1 count is 2
c2 count is 2
```
* *Static* methods can access only static fields (Doesn't apply on Constructors) If *count* was private we would need a *get* method to access it as follows
```java
public static int getCount() { return count; }
```
* *Static* methods can be called by other classes only by the name of the class
```java
System.out.println("Number of existing circles : " + Circle.getCount());
```
```java
Number of existing circles : 2
```


## Memory allocation of static fields
<img src=media/memory_static.svg width=300 height=500 /></br>
```java
Circle c1 = new Circle();
Circle c2 = new Circle();
```


## The *final* modifier
* In our previous Circle class example we add the following field
```java
/* The unique id of a circle */
private final int id;
```
* We are obliged to initialize the field *id*
```java
/* Modified constructor */
Circle() {
	this.x = 0;
	this.y = 0;
	this.radius = 3;
	count += 1;
	/* we assign the current count as the circle's id */
	id = count; 
}
```
* *final* fields cannot change their value/state after their initialization


## The *final* modifier (continued)
* As in the *static* example, we execute the following commands 

```java
Circle c1 = new Circle();
Circle c2 = new Circle();
Circle c3 = new Circle();

System.out.println("c1 count is " + Circle.getCount() +  ", id is " + c1.getId());
System.out.println("c2 count is " + Circle.getCount() +  ", id is " + c2.getId());
System.out.println("c3 count is " + Circle.getCount() +  ", id is " + c3.getId());
```
* Which result the following output
```java
c1 count is 3, id is 1
c2 count is 3, id is 2
c3 count is 3, id is 3
```

<!--
## The *Utility* class
```java
public final class MyUtilities {
	/* Reads the content of a txt file and store in a list which returns*/
	public static List<String> readFile (String filepath) {
		/* ...read file... */
		return list;
	}

	/* Stores the content of a list in a txt file */ 
	public static void writeFile (List<String> list, String filepath) {
		/* ...store content to file... */
	}
}
```
* **Utility classes should be used with care**
 * Include only general functionalities that are common to many other classes 
-->


## Singleton
```java
class DBConnector
{
	/* unique instance of the class */
	private static DBConnector unique_db_connection_instnce;

	/* Private constructor of the class */
	private DBConnector()
	{
		... 
	}

	/* method that creates (if not initialized)
	and returns the unique_db_connection_instnce of the class */
	public static  DBConnector getInstance()
	{
		if (unique_db_connection_instnce == null)
			unique_db_connection_instnce = new DBConnector();

		return unique_db_connection_instnce;
	}

	/* sample method */
	public void connect()
	{
		...	
	}
}
```
* Only **one** instance of a Singleton class can exist at a time
* The constructor is *private*


## Classes as custom types
```java
class Laptop {
	/* The serial number of the product */
	private String serialNumber;
	/* Custom class representing the central processor unit */
	private Cpu cpu;
	/* Custom class representing the random access memory */ 
	private Memory memory;
	/* Custom class representing the Operating system license
	   The license is bound to this Laptop object */
	private OSLicense osLicense;
}
```
* Custom types behave as normal primitive type fields 


## Classes as custom types (continued)
```java
class Laptop {
	private String serialNumber;
	private Cpu cpu;
	private Memory memory;
	private OSLicense osLicense;

	/* Constructor */
	Laptop () {
		this.serial_number = "XXXX-XXXX-XXXX-XXXX";
		this.cpu = new Cpu();
		this.memory = new Memory();
		//osLicense is not initialized
	}
}
```
* Not initialized objects have the *null* value


## *Deep* vs *shallow* copies
* Copying complex objects (that have other non-primitive types as instance variables) can be tricky. If we copy only the top object of the hierarchy we end up having a **shallow copy** of the object, as shown in slide *"Memory allocation"*
<br>
* In order to have a complete (**deep**) copy of this object, we need to ensure that all objects (in all hierarchies) are also copied properly, with their copy constructors. 
<br>
* Avoid using the *clone()* method that all objects *inherit* from their *Object* superclass if you haven't properly *overidden* them. 


## Packages
<!-- ![](media/packages.png) -->
<img src=media/packages.png width=400 height=400 /></br>
* Groups of related parts (Classes) of a system
* Provide access control to classes between other packages


## Relationship among classes
<img src=media/laptop_class_diagram.png width=660 height=510 /></br>


## Simple dependency
<img src=media/dependency.png width=700 height=300 /></br>
* An instance *b* of type *ClassB* is used and exists only in the scope of a method of ClassA


## Association/Aggregation
<img src=media/association.png width=700 height=300 /></br>
* ClassA holds an instance of ClassB
* The aggregated object *b* can live even after the destruction of the ClassA's instance

<!--
## Aggregation
<img src=media/aggregation.png width=700 height=300 /></br>
* ClassA, like in *Association* holds an instance of ClassB
* The aggregated object *b* can live even after the destruction of the ClassA's instance 
-->


## Composition
<img src=media/multiplicity.png width=700 height=300 /></br>
* ClassA, like in *Association/Aggregation* holds an instance of ClassB
* ClassA is responsible for object's *b* lifecycle and object *b* should be destroyed upon ojbect's *a* destruction. 


## References
* Thinking in Java (4th Edition) - B. Eckel
* Object Oriented Design - A. Chatzigeorgiou
* Oracle Certified Professional Java SE 8 Programmer Exam 1Z0-809, A Comprehensive OCPJP 8 Certification Guide - S. G. Ganesh, Hari Kiran, Tushar Sharma
* Java Programming - wikibooks ([link](https://en.wikibooks.org/wiki/Java_Programming))
* Java™ Platform, Standard Edition 8 API Specification ([link](https://docs.oracle.com/javase/8/docs/api/))
* Contact details
 * email: antoniosgkortzisATgmailDOTcom
 * slack: agkortzis 


## Exercise 1
* **Step 1**: Create a class that represents a circle shape. The class should be named as *Circle* and include the following three integer fields:
 * *x* : the x coordinate
 * *y* : the y coordinate
 * *r* : the radius
<br>
Choose appropriate access modifiers for the fields so that they cannot be accessed by other classes. 


## Exercise 1 (continued)
* **Step 2**: Create methods that provide access and modification (getters and setters) to the *x*, *y* and *r* fields. 
 * Choose appropriate names that briefly describe the functionality of each method
 * Choose appropriately the return type and access modifiers of your methods


## Exercise 1 (continued)
* **Step 3**: Create a default *constructor* that initializes a Circle to x=y=0 and r=5 
* **Step 3.1**: Create an overloaded *constructor* that initializes all three instance variables
* **Step 4**: Create a method *printCircleDetails* that prints the details of your circle in the following message
		* I'm a circle at point (x,y) with radius r
Where *x*,*y* and *r* are the values of the current circle


## Exercise 1 (continued)
* **Step 5**: Create a new class named *TestCircles* in the same package (directory) as your *Circle* class.
* Create a *main* method in your *TestCircles* class. In the *main* method:
 * create a circle object,
 * assign values (of your preference) to the object using the setter methods from *Step 2* and
 * print the details of your circle using the *printCircleDetails* method from *Step 3*
<br><br>
* **Compile and run your program!**


## Exercise 1 (continued)
* **Step 6**: Create an overloaded constructor which will initialize the x & y instance variables. The r instance variable should be initialized by calling the constructor from **Step 3**
* In your *main* method, create objects using each one of the (now three) available constructors and print (using the *print* method) your objects


## Exercise 1 (continued)
* **Step 7**: Extend the functionality of your class by adding the following two methods:
 * the *calculateArea* which will calculates and returns the area (π\*radius\*radius, π=3.14) and
 * the *calculatePerimeter* which will calculates and returns the perimeter (2\*π\*radius, π=3.14)
* Choose the appropriate return types for your methods
* Test the functionality of the two new methods with the Circles that you created earlier in your main method


## Exercise 1 (continued)
* **Step 8**: Add to your class a *static* and *final* field name *pi* (for π). Initialize its value upon declaring the field. Then, modify your *calculateArea* and *calculatePerimeter* methods of *Step 7* so that they make use of the new *pi* field.


## Exercise 1 (continued)
* **Step 9**: Create a *copy constructor* for your *Circle* class. 
 * Create two circles where the second one will be a copy of the first one
 * Print their details
 * Change the values of the first circle and print again their details
 * What do you observe? Explain your findings according to the *memory allocation* in slide \#17


## Exercise 1 (continued)
* **Step 10**: Create a method name *cocentric* that checks if two circles share the same *centre* (co-centric circles). The method should return *true* if circles are co-centric, or *false* if circles have different centres.
* What is the return type of the method?
* What type of argument should your method have?


## Exercise 1 (continued)
* **Step 11**: Declare a field named *numberOfCreatedCircles* that is common to all instances of class Circle and counts the number of the created circles. Think carefully of:
 * the type of your *numberOfCreatedCircles* field,
 * any special modifiers that might need and,
 * the place/places that the value of the field should be incremented  


## Exercise 2
* Create a *class diagram* (on paper or any other tool) for the relation among the following entities (Each entity is a *Class*):
 * There is a *Car* that has a *CarLicense*. The *CarLicense* cannot exist without a *Car*.
 * There is a *Driver* that owns (only one) *DriversLicense*. The *DriversLicense* cannot exist without a *Driver*.
 * The *Driver* owns one or more *Car*s. The *Car* exists even without a *Driver*.


## Exercise 2 (continued)
* Use the correct *UML connectors* for the above relations among the entities
* Create the skeleton source code for the above classes (no need for fields, constructors or methods) and compile it


## Exercise 3
You have the following relations between entities:
* There is a *Library* that has a collection (single dimension array) of *Book*s
* Each *Book* has an *Author*
* The *Library* is operated by a *Librarian*
* The user can make requests regarding authors' and book availability only by asking the Librarian
* For all of the following classes, additional to the requirements described in the slides, create the **getter and setter methods** (only where is needed) for interacting with their instance variables and any necessary **constructors** 


## Exercise 3 (continued)
* **Class Author**
* Fields: 
 * **name**, of type *String*
* Methods: 
 * **toString**, return type String, returns the name of the author 


## Exercise 3 (continued)
* **Class Book**
* Fields: 
 * **title**, type String, 
 * **author**, type Author,
 * **isbn**, type String,
 * **physicalCopies**, type int,
 * **availableCopies**, type int, and 
 * **timesRented**, type int
* **Important** : 
 * **isbn** cannot change after the initialization


## Exercise 3 (continued)
* **Class Book**
* Methods:
 * **toString**, return type String. Returns the details of the book including the Author details. The Authors' details should be acquired by the proper **toString** method
 * **rentPhysicalCopy**, type *void*. Checks if there is an available copy for renting. If yes, then it prints a message of success. **What fields should be modified upon a successful rental?** 
 * **isAvailable**, return type boolean. Checks if there is at least one available physical copy of the book, and
 * **hasAuthor**, return type boolean. Checks if a given name is the name of this book's author


## Exercise 3 (continued)
* **Class Library**
* Fields: 
 * **books**, type Book[] (array of **Books**)
* Methods:
 * **printAvailableBooks**, type *void*. Prints books that have at least one available physical copy. Hint: Use the **isAvailable** and the **toString** methods from the **Book** class
 * **printBookDetails** (Searches for a book based on a given title. If the book exists then its details should be printed, otherwise an error message should be displayed)


## Exercise 3 (continued)
* **Class Library**
* Methods:
 * **printBooksFromAuthor**, type void. Prints only the books that have an author that matches a given name
 * **printTheMostPopularBook**, type void. Prints the book with the highest number of the **timesRented** field.


## Exercise 3 (continued)
* **Class Librarian**
* Fields: 
 * **library**, type **Library**. The library that he manages. 
* Methods:
 * **findMeBooksFromAuthor**, type void. Receives an author name and delegates the request to the library's **printBooksFromAuthor** method
 * **findMeAvailableBooks**, type void. Delegates the request to the library's **printAvailableBooks** method
 * **findMeBook**, type void. Receives a book's title and delegates the request to the library's **printBookDetails** method
 * **findMostPopularBook**, type void. Delegates the request to the library's **printTheMostPopularBook** method 


## Exercise 3 (continued)
* Create a **TestLibrary** class with a **main** method in which you will execute the following code block:
```java
/** Create Random authors */
Author ruth = new Author("Ruth");
Author diane = new Author("Diane");
Author jacqueline = new Author("Jacqueline");
Author rachel = new Author("Rachel");
Author joan = new Author("Joan");
Author theresa = new Author("Theresa");
Author angela = new Author("Angela");
Author helen = new Author("Helen");
Author lisa = new Author("Lisa");
/** Create Random books from the above authors */
Book book1 = new Book("Book1",ruth,"368777540-2",10,2,20);
Book book2 = new Book("Book2",diane,"963099898-2",10,1,22);
Book book3 = new Book("Book3",jacqueline,"005382097-2",10,0,23);
Book book4 = new Book("Book4",rachel,"538310208-2",10,3,24);
Book book5 = new Book("Book5",joan,"562448132-2",10,4,26);
Book book6 = new Book("Book6",theresa,"670364563-2",10,2,21);
Book book7 = new Book("Book7",angela,"466916869-2",10,5,17);
Book book8 = new Book("Book8",helen,"764674973-2",10,0,15);
Book book9 = new Book("Book9",lisa,"052469721-2",10,6,17);
Book book10 = new Book("Book10",ruth,"609291817-2",10,3,13);
Book book11 = new Book("Book11",diane,"451378028-2",10,8,12);
Book book12 = new Book("Book12",jacqueline,"142352773-2",10,6,20);
Book book13 = new Book("Book13",rachel,"115135166-2",10,0,20);
Book book14 = new Book("Book14",joan,"631942468-2",10,3,20);
Book book15 = new Book("Book15",theresa,"323662444-2",10,0,23);
Book book16 = new Book("Book16",angela,"121360492-2",10,0,12);
Book book17 = new Book("Book17",helen,"391199302-2",10,0,20);
Book book18 = new Book("Book18",ruth,"549307784-2",10,1,20);
Book book19 = new Book("Book19",ruth,"368777230-2",10,23,20);
Book book20 = new Book("Book20",ruth,"793027213-2",10,0,20);
/** Add the books to a Book array*/
Book[] books = {book1,book2,book3,book4,book5,book6,book7,
book8,book9,book10,book11,book12,book13,book14,book15,
book16,book17,book18,book19,book20};/** Assign the book collection to the library */
Library library = new Library(books);
/** Librarian, theGuyWhoKnowsAlot, undertakes the operation of the library */
Librarian theGuyWhoKnowsAlot = new Librarian(library);
theGuyWhoKnowsAlot.findMeAvailableBooks();
theGuyWhoKnowsAlot.findMeBook("Book3");
theGuyWhoKnowsAlot.findMeBooksFromAuthor("Ruth");
theGuyWhoKnowsAlot.findMostPopularBook();
```
* **Compare your output to the one in the next slide**


## Exercise 3 (end)
* The expected output (format can vary between different implementations) after the running the code from the previous slide is:

```java
The following books are available at the library for renting
Books available for renting:
	1. Book [title=Book1, author=Ruth, isbn=368777540-2, physicalCopies=10, availableCopies=2, timesRented=20]
	2. Book [title=Book2, author=Diane, isbn=963099898-2, physicalCopies=10, availableCopies=1, timesRented=22]
	3. Book [title=Book4, author=Rachel, isbn=538310208-2, physicalCopies=10, availableCopies=3, timesRented=24]
	4. Book [title=Book5, author=Joan, isbn=562448132-2, physicalCopies=10, availableCopies=4, timesRented=26]
	5. Book [title=Book6, author=Theresa, isbn=670364563-2, physicalCopies=10, availableCopies=2, timesRented=21]
	6. Book [title=Book7, author=Angela, isbn=466916869-2, physicalCopies=10, availableCopies=5, timesRented=17]
	7. Book [title=Book9, author=Lisa, isbn=052469721-2, physicalCopies=10, availableCopies=6, timesRented=17]
	8. Book [title=Book10, author=Ruth, isbn=609291817-2, physicalCopies=10, availableCopies=3, timesRented=13]
	9. Book [title=Book11, author=Diane, isbn=451378028-2, physicalCopies=10, availableCopies=8, timesRented=12]
	10. Book [title=Book12, author=Jacqueline, isbn=142352773-2, physicalCopies=10, availableCopies=6, timesRented=20]
	11. Book [title=Book14, author=Joan, isbn=631942468-2, physicalCopies=10, availableCopies=3, timesRented=20]
	12. Book [title=Book18, author=Ruth, isbn=549307784-2, physicalCopies=10, availableCopies=1, timesRented=20]
	13. Book [title=Book19, author=Ruth, isbn=368777230-2, physicalCopies=10, availableCopies=23, timesRented=20]
Book with title= 'Book3' found! Details: 
	Book [title=Book3, author=Jacqueline, isbn=005382097-2, physicalCopies=10, availableCopies=0, timesRented=23]
Book with author= 'Ruth' found! Details:
	Book [title=Book1, author=Ruth, isbn=368777540-2, physicalCopies=10, availableCopies=2, timesRented=20]
Book with author= 'Ruth' found! Details:
	Book [title=Book10, author=Ruth, isbn=609291817-2, physicalCopies=10, availableCopies=3, timesRented=13]
Book with author= 'Ruth' found! Details:
	Book [title=Book18, author=Ruth, isbn=549307784-2, physicalCopies=10, availableCopies=1, timesRented=20]
Book with author= 'Ruth' found! Details:
	Book [title=Book19, author=Ruth, isbn=368777230-2, physicalCopies=10, availableCopies=23, timesRented=20]
Book with author= 'Ruth' found! Details:
	Book [title=Book20, author=Ruth, isbn=793027213-2, physicalCopies=10, availableCopies=0, timesRented=20]
Most popular book: 
	Book [title=Book5, author=Joan, isbn=562448132-2, physicalCopies=10, availableCopies=4, timesRented=26]
Book with title:'Book0' not found
Book with author:'angor' not found

```


## Exercise 4 (BONUS!)
* Create a command-line user interface for Exercise 3, providing the user, at least, the following options:
		Welcome to the Bootcamp library. 
		How do you want to proceed?
		1. Show all available books
		2. Search for a book (by book title)
		3. Display books from a specific author
		4. Show me the most popular book
		q. Quit
		> 

* Create (a fully detailed) **class diagram** for the entities described in exercise 3. 
