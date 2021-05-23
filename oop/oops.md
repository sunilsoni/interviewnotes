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


Does Abstract class have constructor?
------------

Yes, abstract classes have constructor. Either you can provide it or the default one will be provided by Java. Now, you must be wondering if you cannot create an object of abstract class then what is the need of a constructor.
One thing you must know is that the constructors are used when you are creating an object of a class, to initialize the data members of that class and your abstract class can have data members.

Now, when your class extends abstract class then the same abstract class will become super class for your extending class and remember when you have constructor of your class then first line of your constructor is always a call to super class constructor and this is the time when your abstract class constructor will get called.

Example 1:
```java
abstract class MyAbstractClass {

	public MyAbstractClass() {
		System.out.println("inside MyAbstractClass constructor");
	}

}

public class AbstractDemo extends MyAbstractClass {

	public AbstractDemo() {
		System.out.println("inside AbstractDemo constructor");
	}
	
	public static void main(String[] args) {
		AbstractDemo obj = new AbstractDemo();
	}

}
```
Output:
```log
inside MyAbstractClass constructor
inside AbstractDemo constructor
```

Example 2:
```java

abstract class MyAbstractClass {

	public int a;
	public int b;
	
	public MyAbstractClass(int a, int b) {
		this.a = a;
		this.b = b;
	}
	
	public void print() {
		System.out.println("a = " + a);
		System.out.println("b = " + b);
	}

}

public class AbstractDemo extends MyAbstractClass {

	public AbstractDemo(int x, int y) {
		super(x, y);
		
	}
	public static void main(String[] args) {
		AbstractDemo obj = new AbstractDemo(5, 10);
		obj.print();
	}

}
```
Output:

```log
a = 5
b = 10
```

Interface
------------
- An interface in Java is a blueprint of a class. It has static constants and abstract methods.
- Interface specify what a class must do but not how to do
- An interface is like defining a contract that is fulfilled by implementing classes
- An interface is used to achieve full abstraction.
- All methods in an interface are public and abstract by default and all variables declared in an interface are constants i.e. public, static and final
- A class which implements an interface will have to provide implementation of all the methods that are defined in the interface
- A class can implement more than one interface, this is how Java allows multiple inheritance.
- Since Java 8, we can have default and static methods in an interface

Abstract class Vs Interface
------------
The differences are:
- Abstract class can have both abstract and concrete methods but interface can only have abstract methods (Java 8 onwards, it can have default and static methods as well)
- Abstract class methods can have access modifiers other than public but interface methods are implicitly public and abstract
- Abstract class can have final, non-final, static and non-static variables but interface variables are only static and final
- A subclass can extend only one abstract class but it can implement multiple interfaces
- An Abstract class can extend one other class and can implement multiple interfaces but an interface can only extend other interfaces

from Java 8 onwards, you can have static and default methods in an Interface so now what is the difference between abstract class and interface and the answer is – We can still extend only one class but can implement multiple interfaces.

What to choose – interface or abstract class
------------
Consider these points while choosing between the two:
- When you want to provide default implementation to some of the common methods that can be used directly by the sub-classes then you can use abstract class because it can have concrete methods also, this is not the case with Interface because the child classes that are implementing this interface will have to provide implementation for all the methods that are declared in the interface
- If your contract keeps on changing then Interface will create problems because then you will have to provide implementation of those new methods in all the implementing classes, whereas with abstract class you can provide one default implementation to the new methods and only change those implementing classes that are actually going to use these new methods

Most of the times, interfaces are a good choice. It is also one of the best practices, when you code in terms of interfaces.

Why Java 8 has introduced default methods?
------------

To extend the capability of an already existing interface, default methods are introduced in Java 8. Let’s understand this by one example:

Consider there are 100 classes that are implementing one interface. Now you want to define one new method inside your interface. In this case you will have to change all the implementation classes to fulfill the interface contract. So, Java introduced default methods, here you can provide default implementation of that new method inside your interface and as it is not mandatory to provide implementation of default methods by the implementing classes, all the 100 classes can use the default implementation or if they want they can provide their own implementation by overriding the default method.

Now consider one interesting scenario: You have two interfaces, Interface1 and Interface2 both having default method hello() and one class is implementing these 2 interfaces without giving implementation to this default method. You see the problem here? Yes, it is the famous Diamond Problem (Refer to Question 9 , if you’re not already familiar with this problem).
```java
interface Interface1 {
	default void hello() {
		System.out.println("Hello from Interface1");
	}
}

interface Interface2 {
	default void hello() {
		System.out.println("Hello from Interface2");
	}
}

public class Child implements Interface1, Interface2 {
	
}

```
 <img src="./images/default-methods-error.png" width="800" border="2" />

So, to avoid this error, it is mandatory to provide implementation for common default methods of interfaces

```java

public class Child implements Interface1, Interface2 {
	@Override
	public void hello() {
		System.out.println("inside Child class hello method");
		Interface1.super.hello();
	}
	
	public static void main(String[] args) {
		Child obj = new Child();
		obj.hello();
	}
}
```
Output: 
```log
Inside Child class hello method
Hello from Interface1
```

Why Java 8 has introduced static methods?
------------

Consider an example where you want to define a utility class, what you usually do is you define a class which contains static methods and then you call these methods using class name. Now, Java 8 onwards you can do the same thing using an Interface by giving only static methods inside your interface. This way of using Interface for defining utility classes is better as it helps in performance also, because using a class is more expensive operation than using an interface.

Why Java does not allow multiple inheritance?
------------
Multiple inheritance occurs when a class has more than one parent classes.
Why Java does not allow this : let us consider there are 2 parent classes having a method named hello() with same signature and one child class is extending these 2 classes, if you call this hello() method which is same in both parents, which parent class method will get executed – it results into an ambiguous situation, this is also called Diamond Problem .
You will get a compile time error if you try to extend more than one class.


```java
class Parent1 {
	default void hello() {
		System.out.println("Hello from Parent1 class");
	}
}

class Parent2 {
	default void hello() {
		System.out.println("Hello from Parent2 class");
	}
}

public class Child extends Parent1, Parent2 {
	
}

```

Output:
```log
Syntax error on token ",". expected.
```

Method Overloading and Overriding
-------------------------
There are 2 ways by which we can achieve polymorphic behavior

1. Method Overloading
2. Method Overriding


Method Overloading
-------------------
1. Method overloading means two or more methods in a class having the same name but different parameters(arguments).
2. Methods may or may not have a different return type.
3. Method overloading reduces duplicate code and allows us to use the same method name for different purposes.
4. Method overloading is also called Compile time polymorphism because, at the time of compiling the code, the compiler decides which method is going to be called based on the method name, return type, and arguments.
5. Overloading can also happen in the case of inheritance. This is because the Child class already has one version of inherited methods from the parent class and can also write another overloaded version of that method.

Simply put, we can implement method overloading in _two different ways_:
1. implementing two or more methods that have the same name but take different numbers of arguments
2. implementing two or more methods that have the same name but take arguments of different types


Rules for Method Overloading
-------------------
Two methods can be called overloaded if they follow rules:
- Both have same method name
- Both have different arguments

If both methods follow these two rules, then they **may or may not**:
- Have different access modifiers
- Have different return types
- Throw different checked or unchecked exceptions


**Example 1:** Different Numbers of Arguments

The Multiplier class shows how to overload the multiply() method by simply defining two implementations that take different numbers of arguments:

```java
public class Multiplier {
    public int multiply(int a, int b) {
        return a * b;
    }
    public int multiply(int a, int b, int c) {
        return a * b * c;
    }
}
```



**Example 2:** Arguments of Different Types
Similarly, we can overload the multiply() method by making it accept arguments of different types:
```java
public class Multiplier {

    public int multiply(int a, int b) {
        return a * b;
    }

    public double multiply(double a, double b) {
        return a * b;
    }
}

```
it's legitimate to define the Multiplier class with both types of method overloading:
```java
public class Multiplier {

    public int multiply(int a, int b) {
        return a * b;
    }

    public int multiply(int a, int b, int c) {
        return a * b * c;
    }

    public double multiply(double a, double b) {
        return a * b;
    }
}
```
however, that it's not possible to have two method implementations that differ only in their return types.

To understand why – let's consider the one example:

```java
public int multiply(int a, int b) { 
    return a * b; 
}
 
public double multiply(int a, int b) { 
    return a * b; 
}

```
In this case, the code simply **wouldn't compile** because of the method call ambiguity – the compiler wouldn't know which implementation of multiply() to call.


**Example 3:** Type Promotion

One neat feature provided by method overloading is the so-called type promotion, a.k.a. widening primitive conversion.

In simple terms, one given type is implicitly promoted to another one when there's no matching between the types of the arguments passed to the overloaded method and a specific method implementation.

To understand more clearly how type promotion works, consider the following implementations of the multiply() method:


```java
public double multiply(int a, long b) {
    return a * b;
}

public int multiply(int a, int b, int c) {
    return a * b * c;
}


```
Now, calling the method with two int arguments will result in the second argument being promoted to long, as in this case there's not a matching implementation of the method with two int arguments.

Let's see a quick unit test to demonstrate type promotion:
```java
@Test
public void whenCalledMultiplyAndNoMatching_thenTypePromotion() {
    assertThat(multiplier.multiply(10, 10)).isEqualTo(100.0);
}
```

Conversely, if we call the method with a matching implementation, type promotion just doesn't take place:

```java
@Test
public void whenCalledMultiplyAndMatching_thenNoTypePromotion() {
    assertThat(multiplier.multiply(10, 10, 10)).isEqualTo(1000);
}
```


Here's a summary of the type promotion rules that apply for method overloading:
- byte can be promoted to short, int, long, float, or double
- short can be promoted to int, long, float, or double
- char can be promoted to int, long, float, or double
- int can be promoted to long, float, or double
- long can be promoted to float or double
- float can be promoted to double


**Static Binding**
The ability to associate a specific method call to the method's body is known as binding.
In the case of method overloading, the binding is performed statically at compile time, hence it's called static binding.
The compiler can effectively set the binding at compile time by simply checking the methods' signatures.

Method Overriding
-------------------
1. Method overriding is defining a method in the child class with the same method name and same method signature which is already written in the parent class.
2. Return type of overridden method can be a subtype of the return type of parent class method.
   E.g. If the parent class method returns Vehicle then Subclass’s overridden method’s return type can be any subclass of Vehicle class, for example, Car can be a return type of overridden method in child class. (Assuming Vehicle as parent class and Car as a child class of Vehicle class).
3. It can’t have a lower access modifier.
   E.g. If the parent class method has a protected access modifier then the child class overridden method cannot have a private access modifier, but the public is allowed.
4. Use @override annotation for the overridden method, so if we don’t follow the overriding rules then the compiler will show the error.
5. Method overriding is called Dynamic Polymorphism because the method which is going to be called is decided at run time by the JVM.
6. Static methods can’t be overridden, only instance methods are overridden.

Rules for Method Overriding
-------------------
The overriding method of child class must follow below rules:
- It must have same method name as that of parent class method
- It must have same arguments as that of parent class method
- It must have either the same return type or covariant return type (child classes are covariant types to their parents)
- It must not throw broader checked exceptions
- It must not have a more restrictive access modifier (if parent method is public, then child method cannot be private/protected)


**Example:** 

Let's see now how to use method overriding by creating a simple, inheritance-based (“is-a”) relationship.

Lets say `Vehicle` is the base class:

```java
public class Vehicle {
    
    public String accelerate(long mph) {
        return "The vehicle accelerates at : " + mph + " MPH.";
    }
    
    public String stop() {
        return "The vehicle has stopped.";
    }
    
    public String run() {
        return "The vehicle is running.";
    }
}
```
And  a  subclass:

```java
public class Car extends Vehicle {

    @Override
    public String accelerate(long mph) {
        return "The car accelerates at : " + mph + " MPH.";
    }
}
```
In this hierarchy , we've simply overridden the `accelerate()` method in order to provide a more refined implementation for the subtype Car.

Here, it's clear to see that if an application uses instances of the Vehicle class, then it can work with instances of Car as well, as both implementations of the `accelerate()` method have the same signature and the same return type.

Let's unit tests to check the Vehicle and `Car` classes:

```java
@Test
public void whenCalledAccelerate_thenOneAssertion() {
    assertThat(vehicle.accelerate(100))
      .isEqualTo("The vehicle accelerates at : 100 MPH.");
}
    
@Test
public void whenCalledRun_thenOneAssertion() {
    assertThat(vehicle.run())
      .isEqualTo("The vehicle is running.");
}
    
@Test
public void whenCalledStop_thenOneAssertion() {
    assertThat(vehicle.stop())
      .isEqualTo("The vehicle has stopped.");
}

@Test
public void whenCalledAccelerate_thenOneAssertion() {
    assertThat(car.accelerate(80))
      .isEqualTo("The car accelerates at : 80 MPH.");
}
    
@Test
public void whenCalledRun_thenOneAssertion() {
    assertThat(car.run())
      .isEqualTo("The vehicle is running.");
}
    
@Test
public void whenCalledStop_thenOneAssertion() {
    assertThat(car.stop())
      .isEqualTo("The vehicle has stopped.");
}
```
Now, let's see some unit tests that show how the run() and stop() methods, which aren't overridden, return equal values for both Car and Vehicle:

```java
@Test
public void givenVehicleCarInstances_whenCalledRun_thenEqual() {
    assertThat(vehicle.run()).isEqualTo(car.run());
}
 
@Test
public void givenVehicleCarInstances_whenCalledStop_thenEqual() {
   assertThat(vehicle.stop()).isEqualTo(car.stop());
}
```
In our case, we have access to the source code for both classes, so we can clearly see that calling the accelerate() method on a base Vehicle instance and calling accelerate() on a Car instance will return different values for the same argument.

Therefore, the following test demonstrates that the overridden method is invoked for an instance of Car:

```java
@Test
public void whenCalledAccelerateWithSameArgument_thenNotEqual() {
    assertThat(vehicle.accelerate(100))
      .isNotEqualTo(car.accelerate(100));
}
```

**Type Substitutability**
It's valid to make an overridden method to accept arguments of different types and return a different type as well, but with full adherence to these rules:

- If a method in the base class takes argument(s) of a given type, the overridden method should take the same type or a supertype (a.k.a. contravariant method arguments)
- If a method in the base class returns void, the overridden method should return void
- If a method in the base class returns a primitive, the overridden method should return the same primitive
- If a method in the base class returns a certain type, the overridden method should return the same type or a subtype (a.k.a. covariant return type)
- If a method in the base class throws an exception, the overridden method must throw the same exception or a subtype of the base class exception

**Dynamic Binding**

Considering that method overriding can be only implemented with inheritance, where there is a hierarchy of a base type and subtype(s), the compiler can't determine at compile time what method to call, as both the base class and the subclasses define the same methods.

As a consequence, the compiler needs to check the type of object to know what method should be invoked.

As this checking happens at runtime, method overriding is a typical example of dynamic binding.


For more information:
1. [Method Overloading and Overriding in Java](https://www.baeldung.com/java-method-overload-override)
2. [What Is Method Overloading and Method Overriding in Java?](https://medium.com/javarevisited/what-is-method-overloading-and-method-overriding-in-java-b3b094267fce)