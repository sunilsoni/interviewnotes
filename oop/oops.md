Object-oriented programming(OOPS)
=======
> Object-oriented programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data and code: data in the form of fields (often known as attributes or properties), and code, in the form of procedures (often known as methods).

4 pillars of OOPS are:
1. Abstraction
2. Encapsulation
3. Inheritance
4. Polymorphism

Let’s take a look at them:

Abstraction
------------
Abstraction is a process of hiding the implementation details and showing only functionality to the user. 

Real world examples:
- TV remote: To start the TV, you have to press the power button, you don’t have to know about the internal circuit operations like how infrared waves are passing.
- Car gears: We know what happens when we change the gear. But we don’t know how changing gear works under the hood, that information is irrelevant to us, so it is abstracted.

In java, Abstraction can be achieved in two ways:
- Abstract classes
- Interfaces

Encapsulation
------------
Encapsulation is a process of Binding data and methods within a class . Think of it like showing the essential details of a class by using the access control modifiers (public, private, protected ). So, we can say that Encapsulation leads to the desired level of Abstraction.

Example:
Java Bean, where all data members are made private and you define certain public methods to the outside world to access them.

Inheritance
------------
Using inheritance means defining a parent-child relationship between classes, by doing so, you can reuse the code that is already defined in the parent class. Code reusability is the biggest advantage of Inheritance.

Java does not allow multiple inheritance through classes but it allows it through interfaces.

Polymorphism
------------
Poly means many and Morph means forms. Polymorphism is the process in which an object or function takes different forms. There are 2 types of Polymorphism :

- Compile Time Polymorphism (Method Overloading)
- Run Time Polymorphism (Method Overriding)

In Method overloading, two or more methods in one class have the same method name but different arguments. It is called as Compile time polymorphism because it is decided at compile time which overloaded method will be called.      

Overriding means when we have two methods with same name and same parameters in parent and child class. Through overriding, child class can provide specific implementation for the method which is already defined in the parent class.


Abstract Class
------------
A class that is declared using “abstract” keyword is known as abstract class. It can have abstract methods (methods without body) as well as concrete methods (methods with body).

Some points to remember:
- An abstract class cannot be instantiated, which means you are not allowed to create an object of the abstract class. This also means, an abstract class has no use unless it is extended by some other class
- If there is any abstract method in a class then that class must be declared abstract
- The first non-abstract class which is extending from an abstract class will have to give implementation of the abstract methods defined in abstract class

Example: 
```java
package com.tech;

abstract class MyAbstractClass {
	//abstract method
	abstract void print();
	//concrete method
	public void display() {
		System.out.println("In display method");
	}
}
```

```java
public class AbstractDemo extends MyAbstractClass {
	@Override
	void print() {
		System.out.println("In print method");
	}
	public static void main(String[] args) {
		AbstractDemo obj = new AbstractDemo();
		obj.print();
		obj.display();
	}
}
```

Output:
```log
 In print method
 In display method
```






















