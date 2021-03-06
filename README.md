# Polymorphism and C++

## Table of Contents

1.  Review
2. C++ Polymorphism
3. Virtual 

---
---

## Review

Happens mostly when we have a hierarchical inheritance  

* One common granparent and a lot of spawn that comes out of this
* When we have a group of classes that are no more complex than the others, however, they are expressed differently
	- a new type of inheritance of the same class
	
The change/difference at the same level of inheritance

A base class like animal with many others

*  Dogs -> Class -> Breed
*  Automobile -> Car -> Type of Car


## Mechanisms
"IS A" relationship  

* Established between two classes where one inherits from another
* B inherits from A, therefore B "is a" A
* Objects that "IS A" another object can be stored in references to the parent object

Overriding

*  When we redefine a method that exists in the parent class with a specialized version in the class
*  In Java this is automatic, however, not in C++
	-  Remember that this is different from Overloading
	
Redefinition vs changing of parameters, Override and Overload respectively


## C++ Polymorphism
IS A relationship is already established, no extra code required  
Overriding requires the use of a keyword

Virtual Keyword

* The virtual keyword allows us to mark a method as overridable
* Like friendship this is a system permission rather than something implicit
	- Similar to the diamond issue from inheritance
	
Instead of Java opt-out with const keyword (final) we have to *opt-in* with C++

## Virtual
Without the virtual keyword, the execution will default to the parent method's definition

*  This is known as static resolution, static linkage or early binding
	-  Different than the static keyword
* Function call is fixed before execution occurs

The virtual keyword tells the compile to examining the nature of the object and call appropriate method instead

* dynamic resolution

### Virtual vs Pure Virtual
Create a method within the parent class to be a default behavior

* This allows special creation when they need to be made, and rely on the parent and others sometimes

This can also be taken to create an Abstract base or Pure Virtual Method

* When dealing in Pure Virtual, a method is created with no explicit definition
* Exists only for the child to implement
* Still defined in the parent for every child to inherit

Pure Virtual methods have no definition in the parent

### Consequences of Pure Virtual
First:

* Any class that contains a declaration for pure virtual method is labeled an Abstract Base Class
* Abstract Base Classes CANNOT be instantiated
* Attempting to instantiate an object of an ABC will cause compilation error

Second:

* Any class that inherits from the Abstract Base Class must provide definition for the Pure Virtual Class methods
* if not they are considered an Abstract Base Class and suffer from consequence one

### Pure Virtual - *Interface*
C++ doesn't have interfaces in the same way as Java

Interface in Java:

* a "tack on" to a class that contains consts and undefined public methods
* The class that implements an interface MUST provide definitions for the interface's methods

In C++ interfaces are created through the use of Pure Virtual Methods and multiple inheritance	
The Abstract Base Class could consist of Pure Virtual methods and those methods MUST be defined by the child

Interface Class:

* No properties, all Pure Virtual Methods
* Usually public

### Pure Virtual Within a Body
Pure Virtual methods can be marked with =0 and provide a body	
Different than interfaces in Java	
Java interfaces cannot have a body in their methods

```cpp
virtual const char* speak() = 0
//The  = 0 means this function is pure virtual
{

	return "hello"; //even though it has a body

}
```

The child class is still forced to implement the pure virtual ... but it doesn’t necessarily have to provide its own definition	
It can use `::` and call on the parent classes definition

## Object Slicing
The "IS A" relationship isn't perfect	
When using a Base Class reference, the compiler ONLY knows about the base class methods  
When assigning a derived class to a base class reference, the expanded portion of the derived class is "sliced off"	

* `child obj;`
* `Parent par = obj;`
* SLICING OCCURS

This can be avoided with pointers	

* Using object references and pointers slicing doesn't occur
	- however, slicing can be caused on accident when passed by value
	
---
---
