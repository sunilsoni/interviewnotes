Java 8
====


New features
-----------
- **Lambda Expressions** − a new language feature allowing treating actions as objects •Method References − enable defining Lambda Expressions by referring to methods directly using their names
- **Optional** − This class is to provide a type-level solution for representing optional values instead of using null references.
- **Functional Interface** – an interface with maximum one abstract method, implementation can be provided using a Lambda Expression
- **Default methods** − give us the ability to add full implementations in interfaces besides abstract methods
- **Nashorn, JavaScript Engine** − Java-based engine for executing and evaluating JavaScript code
- **Stream API** − a special iterator class that allows processing collections of objects in a functional manner
- **Date and Time API** − an improved, immutable JodaTime-inspired Date API

Lambda Expressions
-----------
- Lambda Expression facilitates functional programming and simplifies the development a lot.
- It provides a clear and concise way to represent one method interface using an expression. It is very useful in the collection library. It helps to iterate, filter, and extract data from the collection.
- The Lambda expression is used to provide the implementation of an interface that has a functional interface. It saves a lot of code. In the case of the lambda expression, we don't need to define the method again for providing the implementation. Here, we just write the implementation code.
- Java lambda expression is treated as a function, so the compiler does not create a `.class` file.

- Lambda expressions have three parts: a list of parameters, and arrow, and a body: `(Object o) -> System.out.println(o)`;
- You can think of lambda expressions as anonymous methods (or functions) as they don't have a name.
- A lambda expression can have zero (represented by empty parentheses), one or more parameters.
- The type of the parameters can be declared explicitly, or it can be inferred from the context.
- If there is a single parameter, the type is inferred, and is not mandatory to use parentheses.
- If the lambda expression uses as a parameter name which is the same as a variable name of the enclosing context, a compile error is generated.
- If the body has one statement, curly brackets are not required, and the value of the expression (if any) is returned.
- If the body has more than one statement, curly brackets are required, and if the expression returns a value, it must return with a return statement.
- If the lambda expression doesn't return a result, a return statement is optional.
- The signature of the abstract method of a functional interface provides the signature of a lambda expression.
- In order to use a lambda expression, you first need a functional interface.
- However, lambda expressions don't contain the information about which functional interface are implementing.
- The type of the expression is deduced from the context in which the lambda is used. This type is called a target type.
- The contexts where the target type of a lambda expression can be inferred include an assignment, method or constructor arguments, and a cast expression.
- Default methods of a functional interface cannot be accessed from within lambda expressions.


Why use Lambda Expression
-----------
- To provide the implementation of the Java 8 Functional Interface.
- Less coding.
- Lambda Expressions enable you to encapsulate a single unit of behavior and pass it to other code. You can use lambda expressions if you want a certain action performed on each element of a collection, when a process is completed, or when a process encounters an error.

Lambda Expressions Syntax
-----------
Java Lambda Expression Syntax
```java
(argument-list) -> {body}  
```

Java lambda expression consists of three components.
- **Argument-list**: It can be empty or non-empty as well.
- **Arrow-token**: It is used to link arguments-list and body of expression.
- **Body:** It contains expressions and statements for the lambda expression.

Java Lambda Expression Syntax :
-----------

- Generic Java Lambda Expression Syntax `(argument-list) -> {body} `
- Java Lambda Expression with No Parameter: `() -> { Systen.out.printIn("Lamda Expression"); };`
- Java Lambda Expression with Single Parameter `(msg) -> system.om.printin(msg); } `
- Java Lambda Expression with Multiple Parameters: `(int a,int b) -> (a+b);` 
- Java Lambda Expression without return keyword: `(a, b) -> (a + b); `
- Java Lambda Expression with Multiple Statements:

```java
(x,r) -> { 
    Systen.out.println("x: " : + x);
    Systen.out.printIn("Y :" + y); 
    return (x+y); 
};
``` 

Lambda Expressions Examples
-----------


Functional Interface
-----------
- An Interface that contains exactly one abstract method is known as a functional interface.
- It can have any number of `default`, `static` methods but can contain only one abstract method. It can also declare methods of the object class.
- Functional Interface is also known as Single Abstract Method Interfaces or SAM Interfaces. It is a new feature in Java 8, which helps to achieve a functional programming approach.
- A functional interface can extend another interface only when it does not have any abstract method.
- The Java API has many one-method interfaces such as `Runnable`, `Callable`, `Comparator`, `ActionListener`, and others. They can be implemented and instantiated using anonymous class syntax.

-  A functional interface is an interface that has exactly one abstract method.
-  Since default methods have an implementation, they are not abstract so a functional interface can have any number of them.
-  If an interface declares an abstract method with the signature of one of the methods of java.lang.Object, it doesn't count toward the functional interface method count.
-  A functional interface is valid when it inherits a method that is equivalent but not identical to another.
-  An empty interface is not considered a functional interface.
-  A functional interface is valid even if the @FunctionalInterface annotation would be omitted.
-  Functional interfaces are the basis of lambda expressions

Custom Functional Interface
-----------

```java
@FunctionalInterface
interface Sayable{
    void say(String msg);   // abstract method   
} 
```

```java
public class FunctionalInterfacesExample {

    public static void main(String[] args) {

        Sayable sayable = (msg) -> {
            System.out.println(msg);
        };
        sayable.say("Say something ..");
    }
}  
```



Predefined Functional Interfaces
-----------
Java 8 provides predefined functional interfaces to deal with functional programming by using lambda and method references.

```java
@Setter
@Getter
public class Person {
    private String name;
    private int age;
    public Person(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
}
```

Predicate
-----------



Function
-----------

Supplier
-----------

Consumer
-----------

BiFunction
-----------

BiConsumer
-----------


















For more information:
1. [Java 8 Lambda Expressions](https://www.javaguides.net/2018/07/java-8-lambda-expressions.html)




























