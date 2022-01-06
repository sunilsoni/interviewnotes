Java 8
======

New features
------------

- **Lambda Expressions** − a new language feature allowing treating actions as objects •Method References − enable
  defining Lambda Expressions by referring to methods directly using their names
- **Optional** − This class is to provide a type-level solution for representing optional values instead of using null
  references.
- **Functional Interface** – an interface with maximum one abstract method, implementation can be provided using a
  Lambda Expression
- **Default methods** − give us the ability to add full implementations in interfaces besides abstract methods
- **Nashorn, JavaScript Engine** − Java-based engine for executing and evaluating JavaScript code
- **Stream API** − a special iterator class that allows processing collections of objects in a functional manner
- **Date and Time API** − an improved, immutable JodaTime-inspired Date API

# Lambda Expressions

A lambda expression is an unnamed block of code (or an unnamed function) with a list of formal parameters and a body.
Sometimes a lambda expression is simply called a lambda. The body of a lambda expression can be a block statement or an
expression. An arrow (->) is used to separate the list of parameters and the body.

## Examples of lambda expressions

Takes an int parameter and returns the parameter value incremented by 1

> (int x) -> x + 1

Takes two int parameters and returns their sum

> (int x, int y) -> x + y

Takes two int parameters and returns the maximum of the two

> (int x, int y) -> { int max = x > y ? x : y;
> return max;
> }

Takes no parameters and returns void

> () -> { }

Takes no parameters and returns a string "OK"

> () -> "OK"

Takes a String parameter and prints it on the standard output

> (String msg) -> { System.out.println(msg); }

Takes a parameter and prints it on the standard output

> msg -> System.out.println(msg)

Takes a String parameter and returns its length

> (String str) -> str.length()

```java
@FunctionalInterface
interface StringToIntMapper {
    int map(String str);
}

    StringToIntMapper mapper = (String str) -> str.length();

    String name = "Kristy";
    int mappedValue = mapper.map(name);
System.out.println("name="+name+", mapped value="+mappedValue);
```

Output:

```log
name=Kristy, mapped value=6
```

The following snippet of code uses an anonymous class to achieve the same result as the lambda expression used in the
previous example:

```java
StringToIntMapper mapper=new StringToIntMapper(){
@Override
public int map(String str){
        return str.length();
        }
        };

        String name="Kristy";
        int mappedValue=mapper.map(name);
        System.out.println("name="+name+", mapped value="+mappedValue);
```

Output:

```log
name=Kristy, mapped value=6
```

- Lambda Expression facilitates functional programming and simplifies the development a lot.
- It provides a clear and concise way to represent one method interface using an expression. It is very useful in the
  collection library. It helps to iterate, filter, and extract data from the collection.
- The Lambda expression is used to provide the implementation of an interface that has a functional interface. It saves
  a lot of code. In the case of the lambda expression, we don't need to define the method again for providing the
  implementation. Here, we just write the implementation code.
- Java lambda expression is treated as a function, so the compiler does not create a `.class` file.
- Lambda expressions have three parts: a list of parameters, and arrow, and a
  body: `(Object o) -> System.out.println(o)`;
- You can think of lambda expressions as anonymous methods (or functions) as they don't have a name.
- A lambda expression can have zero (represented by empty parentheses), one or more parameters.
- The type of the parameters can be declared explicitly, or it can be inferred from the context.
- If there is a single parameter, the type is inferred, and is not mandatory to use parentheses.
- If the lambda expression uses as a parameter name which is the same as a variable name of the enclosing context, a compile error is generated.
- If the body has one statement, curly brackets are not required, and the value of the expression (if any) is returned.
- If the body has more than one statement, curly brackets are required, and if the expression returns a value, it must
  return with a return statement.
- If the lambda expression doesn't return a result, a return statement is optional.
- The signature of the abstract method of a functional interface provides the signature of a lambda expression.
- In order to use a lambda expression, you first need a functional interface.
- However, lambda expressions don't contain the information about which functional interface are implementing.
- The type of the expression is deduced from the context in which the lambda is used. This type is called a target type.
- The contexts where the target type of a lambda expression can be inferred include an assignment, method or constructor
  arguments, and a cast expression.
- Default methods of a functional interface cannot be accessed from within lambda expressions.

Why use Lambda Expression
-------------------------

- To provide the implementation of the Java 8 Functional Interface.
- Less coding.
- Lambda Expressions enable you to encapsulate a single unit of behavior and pass it to other code. You can use lambda
  expressions if you want a certain action performed on each element of a collection, when a process is completed, or
  when a process encounters an error.

Lambda Expressions Syntax
-------------------------

Java Lambda Expression Syntax

```java
(argument-list)->{body}
```

Java lambda expression consists of three components.

- **Argument-list**: It can be empty or non-empty as well.
- **Arrow-token**: It is used to link arguments-list and body of expression.
- **Body:** It contains expressions and statements for the lambda expression.

A lambda expression consists of a list of parameters and a body separated by an arrow (->). The list of parameters is
declared the same way as the list of parameters for methods. The list of parameters is enclosed in parentheses, as is
done for methods. The body of a lambda expression is a block of code enclosed in braces. Like a method’s body, the body
of a lambda expression may declare local variables; use statements including break, continue, and return; throw
exceptions, etc. Unlike a method, a lambda expression does not have the following four parts:

• A lambda expression does not have a name. • A lambda expression does not have a return type. It is inferred by the
compiler from the context of its use and from its body. • A lambda expression does not have a throws clause. It is
inferred from the context of its use and its body. • A lambda expression cannot declare type parameters. That is, a
lambda expression cannot be generic.

Examples of Lambda Expressions and Equivalent Methods

Java Lambda Expression Syntax :
-------------------------------

- Generic Java Lambda Expression Syntax `(argument-list) -> {body} `
- Java Lambda Expression with No Parameter: `() -> { Systen.out.printIn("Lamda Expression"); };`
- Java Lambda Expression with Single Parameter `(msg) -> system.om.printin(msg); } `
- Java Lambda Expression with Multiple Parameters: `(int a,int b) -> (a+b);`
- Java Lambda Expression without return keyword: `(a, b) -> (a + b); `
- Java Lambda Expression with Multiple Statements:

```java
(x,r) -> {
        Systen.out.println("x: ":+x);
        Systen.out.printIn("Y :"+y);
        return(x+y);
        };
```

Stream
------

Java provides a new additional package in Java 8 called `java.util.stream`. This package consists of classes,
interfaces, and an enum to allows functional-style operations on the elements. You can use stream by importing
java.util.stream package in your programs.

Stream features
---------------

- Stream does not store elements. It simply conveys elements from a source such as a data structure, an array, or an I/O
  channel, through a pipeline of computational operations.
- Stream is functional in nature. Operations performed on a stream does not modify its source. For example, filtering a
  Stream obtained from a collection produces a new Stream without the filtered elements, rather than removing elements
  from the source collection.
- Stream is lazy and evaluates code only when required.
- The elements of a stream are only visited once during the life of a stream. Like an Iterator, a new stream must be
  generated to revisit the same elements of the source.

You can use Stream to filter, collect, print, and convert from one data structure to other etc.

## Intermediate and Terminal operations

 <img src="../images/intermediate and terminal operations.png" width="1000" />

### Intermediate vs Terminal operations

- Intermediate operation is lazy while a terminal operation is not. 

- When you invoke an intermediate operation on a stream, the operation is not executed immediately. It is executed only when a terminal operation is invoked on that stream. In a way, an intermediate operation is memorized and is recalled as soon as a terminal operation is invoked. 

- You can chain multiple intermediate operations and none of them will do anything until you invoke a terminal operation. At that time, all of the intermediate operations that you invoked earlier will be invoked along with the terminal operation.

- All intermediate operations return Stream (can be chained), while terminal operations don't.

### Intermediate Operations
- filter(Predicate<T>)
- map(Function<T>)
- flatMap(Function<T>)
- sorted(Comparator<T>)
- peek(Consumer<T>)
- distinct()
- limit(long n)
- skip(long n)

### Terminal Operations
- forEach
- forEachOrdered
- toArray
- reduce
- collect
- min
- max
- count
- anyMatch
- allMatch
- noneMatch
- findFirst    
- findAny

Functional Interface
--------------------

- An Interface that contains exactly one abstract method is known as a functional interface.
- It can have any number of `default`, `static` methods but can contain only one abstract method. It can also declare
  methods of the object class.
- Functional Interface is also known as Single Abstract Method Interfaces or SAM Interfaces. It is a new feature in Java
  8, which helps to achieve a functional programming approach.
- A functional interface can extend another interface only when it does not have any abstract method.
- The Java API has many one-method interfaces such as `Runnable`, `Callable`, `Comparator`, `ActionListener`, and
  others. They can be implemented and instantiated using anonymous class syntax.
- A functional interface is an interface that has exactly one abstract method.
- Since default methods have an implementation, they are not abstract so a functional interface can have any number of
  them.
- If an interface declares an abstract method with the signature of one of the methods of java.lang.Object, it doesn't
  count toward the functional interface method count.
- A functional interface is valid when it inherits a method that is equivalent but not identical to another.
- An empty interface is not considered a functional interface.
- A functional interface is valid even if the @FunctionalInterface annotation would be omitted.
- Functional interfaces are the basis of lambda expressions

Custom Functional Interface
---------------------------

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
--------------------------------

Java 8 provides predefined functional interfaces to deal with functional programming by using lambda and method
references.

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
---------

We need a function for checking a condition. A Predicate is one such function accepting a single argument to evaluate to
a boolean result. It has a single method test that returns the boolean value.

Internal implementation of the Predicate interface: Predicate interface contains exactly one abstract method test(T t).
Note that it also contains a default, static methods.

```java
@FunctionalInterface
public interface Predicate<T> {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param t the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(T t);

    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }

    default Predicate<T> negate() {
        return (t) -> !test(t);
    }

    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }

   static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
}
```

Example :

```java
public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Person> predicate = (person) -> person.getAge() > 28;
        boolean result = predicate.test(new Person("James", 29));
        System.out.println(result);
    }
}
```

Function
--------

It represents a function that accepts one argument and returns a result.

The function interface contains exactly one abstract method apply(T t). Note that it also contains a default, static
methods.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);

    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }

    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }

   
    static <T> Function<T, T> identity() {
        return t -> t;
    }
}
```

Example :

```java
import java.util.function.Function;

public class FunctionExample {

    public static void main(String[] args) {
        // convert centigrade to fahrenheit
        Function < Integer, Double > centigradeToFahrenheitInt = x -> new Double((x * 9 / 5) + 32);

        // String to an integer
        Function < String, Integer > stringToInt = x -> Integer.valueOf(x);
        System.out.println(" String to Int: " + stringToInt.apply("4"));


        Function < PersonEntity, PersonDTO > function = (entity) -> {
            return new PersonDTO(entity.getName(), entity.getAge());
        };
        PersonDTO personDTO = function.apply(new PersonEntity("James", 20));
        System.out.println(personDTO.getName());
        System.out.println(personDTO.getAge());
    }
}

class PersonEntity {
    private String name;
    private int age;

    public PersonEntity(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
}

class PersonDTO {
    private String name;
    private int age;

    public PersonDTO(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
}
```

Supplier
--------

Represents a supplier of results.

Internal implementation of the Supplier interface. The supplier interface contains exactly one abstract method get(T t).
Hence we can apply lambda expression to it.

```java
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

Example :

```java
import java.util.function.Supplier;

public class SuppliersExample {

   public static void main(String[] args) {
  
       Supplier<Person> supplier = () -> {
           return new Person("John", 30);
       };

       Person p = supplier.get();
       System.out.println("Person Detail:\n" + p.getName() + ", " + p.getAge());
   }
}
```

Consumer
--------

It represents an operation that accepts a single argument and returns no result. Internal implementation of the Consumer
interface. The consumer interface contains exactly one abstract method accept(T arg0). Hence we can apply lambda
expression to it.

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T arg0);

    default Consumer<T> andThen(Consumer<? super T> arg0) {
       Objects.requireNonNull(arg0);
       return (arg1) -> {
       this.accept(arg1);
       arg0.accept(arg1);
    };
  }
}
```

Example :

```java
public class ConsumersExample {

    public static void main(String[] args) {
        List<Person> listOfPerson = new ArrayList<Person>();
        listOfPerson.add(new Person("abc", 27));
        listOfPerson.add(new Person("mno", 26));
        listOfPerson.add(new Person("pqr", 28));
        listOfPerson.add(new Person("xyz", 27));

        listOfPerson.forEach((person) -> {
            System.out.println(" Person name : " + person.getName());
            System.out.println(" Person age : " + person.getAge());
        });
  
  
        // Second example
        Consumer<Person> consumer = (person) -> {
           System.out.println(person.getName());
           System.out.println(person.getAge());
        };
        consumer.accept(new Person("John", 30));
    }
}
```

BiFunction
----------

To define lambdas with two arguments, we have to use additional interfaces that contain "Bi" keyword in their names: BiFunction, ToDoubleBiFunction, ToIntBiFunction, and ToLongBiFunction.
BiFunction implementation that receives a key and an old value to calculate a new value for the salary and return it.

It represents a function that accepts two arguments and returns a result.
internal implementation of BiFunction interface. BiFunction interface contains exactly one abstract method apply(T arg0, U arg1). Hence we can apply lambda expression to it.

```java
@FunctionalInterface
public interface BiFunction<T, U, R> {
 R apply(T arg0, U arg1);

 default <V> BiFunction<T, U, V> andThen(Function<? super R, ? extends V> arg0) {
  Objects.requireNonNull(arg0);
  return (arg1, arg2) -> {
   return arg0.apply(this.apply(arg1, arg2));
  };
 }
}
```

Example :

```java
public class BiFunctionExample {

    public static void main(String[] args) {
  
       BiFunction<Person, Person, Integer> biFunction = (p1,p2) -> {
           return p1.getAge() + p2.getAge();
       };

        int totalAge = biFunction.apply(new Person("John", 10),
                new Person("James", 10));
        System.out.println(totalAge);

    }
}
```

BiConsumer
----------

It represents an operation that accepts two input arguments and returns no result. Internal implementation of BiConsumer
interface. BiConsumer interface contains exactly one abstract method accept(T arg0, U arg1). Hence we can apply lambda
expression to it.

```java
@FunctionalInterface
public interface BiConsumer<T, U> {
    void accept(T arg0, U arg1);

    default BiConsumer<T, U> andThen(BiConsumer<? super T, ? super U> arg0) {
        Objects.requireNonNull(arg0);
        return (arg1, arg2) -> {
             this.accept(arg1, arg2);
            arg0.accept(arg1, arg2);
        };
     }
}
```

Example :

```java
public class BiConsumersExample {

    public static void main(String[] args) {
  
        BiConsumer<Person, Person> biConsumer = (p1, p2) -> {
             System.out.println(" print first persion");
             System.out.println(p1.getName());
             System.out.println(" print second persion");
             System.out.println(p2.getName());
       };
  
       biConsumer.accept(new Person("John", 10), new Person("James", 10));
    }
}
```

You can also define your own custom functional interface. Following is the list of a functional interface that is placed in java.util.function package.

Method References
-----------------

Method reference is used to refer method of the functional interface. It is a compact and easy form of a lambda expression. Each time when you are using a lambda expression to just referring a method, you can replace your lambda expression with method reference.

Method References Types:
------------------------

- Reference to a static method : `ContainingClass::staticMethodName`
- Reference to an instance method of a particular object : `containingObject::instanceMethodName`
- Reference to an instance method of an arbitrary object of a particular type : `ContainingType::methodName`
- Reference to a constructor: `ClassName::new`

For more information:

1. [Java 8 Lambda Expressions](https://www.javaguides.net/2018/07/java-8-lambda-expressions.html)

