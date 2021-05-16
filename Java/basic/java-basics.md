Java
====


Why String is Immutable?
-----------------------

String is immutable for below reasons:

- **String Pool** : String Pool is possible only because String is Immutable in Java. String pool is a special storage area in Java heap. If the string is already present in the pool, then instead of creating a new object, old object’s reference is returned. This way different String variables can refer to the same reference in the pool, thus saving a lot of heap space also. If String is not immutable then changing the string with one reference will lead to the wrong values to other string variables having the same reference.
- **Security** : String parameters are used in network connections, database URL’s, username and passwords etc. Because String is immutable, these values can’t be changed. Otherwise any hacker could change the referenced values which will cause severe security issues in the application.
- **Multi-threading** : Since String is immutable, it is safe for multithreading. A single String instance can be shared across different threads. This avoids the use of synchronization for thread safety. Strings are implicitly thread-safe.
- **Caching** : The hashcode of string is frequently used in Java. Since string is immutable, the hashcode will remain the same, so it can be cached without worrying about the changes. This makes it a great candidate for using it as a Key in Map.
- **Class Loaders** : Strings are used in Java ClassLoaders and since String is made immutable, it provides security that correct class is being loaded.


StringBuffer and StringBuilder
-----------------------

- Both StringBuffer and StringBuilder classes are used for String manipulation. These are mutable objects. But StringBuffer provides thread-safety as all its methods are synchronized, this makes performance of StringBuffer slower as compared to StringBuilder.

- StringBuffer class is present from Java 1.0, but due to its slower performance, StringBuilder class was introduced in Java 1.5

- If you are in a single-threaded environment or don’t care about thread safety, you should use StringBuilder. Otherwise, use StringBuffer for thread-safe operations.

- You should use String class if you require immutability, use StringBuffer if you require mutability + Thread safety and use StringBuilder if you require mutability and no thread safety.

equals and hashcode contract
-------------

The equals and hashcode contract says:
> If two objects are equals according to equals() method, then their hashcode must be same but reverse is not true i.e. if two objects have same hashcode then they may/may not be equals.


Comparable and Comparator interfaces
---------------------

Both Comparable and Comparator interfaces are used to sort the collection of objects. These interfaces should be implemented by your custom classes, if you want to use Arrays/Collections class sorting methods.
Comparable interface has compareTo(Obj) method, you can override this method in your class, and you can write your own logic to sort the collection.

General rule to sort a collection of objects is:
- If ‘this’ object is less than passed object, return negative integer.
- If ‘this’ object is greater than passed object, return positive integer.
- If ‘this’ object is equal to the passed object, return zero.

- **Comparable Example** :

Employee.java
```java
public class Employee implements Comparable<Employee>{
    private int id;
    private String name;
    private int age;
    private long salary;

    public Employee(int id, String name, int age, long salary) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    public int getId() { return id; }
    public String getName() { return name; }
    public int getAge() { return age; }
    public long getSalary() { return salary; }

    public void setId(int id) {	this.id = id; }
    public void setName(String name) { this.name = name; }
    public void setAge(int age) { this.age = age; }
    public void setSalary(long salary) { this.salary = salary; }

    @Override
    public int compareTo(Employee obj) {
        return this.id - obj.id;
    }

    @Override
    public String toString() {
        return "Employee [id=" + id + ", name=" + name + ", age=" + age + ", "
                + "salary=" + salary + "]" + "\n";
    }

}
```
ComparableDemo.java :
```java

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ComparableDemo {

	public static void main(String[] args) {
		List<Employee> empList = new ArrayList<>();
		
		empList.add(new Employee(4, "Dave", 25, 28000));
		empList.add(new Employee(20, "Mike", 20, 10000));
		empList.add(new Employee(9, "Abhi", 32, 5000));
		empList.add(new Employee(1, "Lisa", 40, 19000));
		
		Collections.sort(empList);
		System.out.println(empList);
	}

}

```

Output:
```log
[Employee [id=1, name=Lisa, age=40, salary=19000]
, Employee [id=4, name=Dave, age=25, salary=28000]
, Employee [id=9, name=Abhi, age=32, salary=5000]
, Employee [id=20, name=Mike, age=20, salary=10000]
]
```

Here, we have sorted the Employee list based on ‘id’ attribute.

- **Comparator Example** :
Now, if we want to sort the employee list based on any other attribute, say name, we will have to change our compareTo() method implementation for this. So, Comparable allows only single sorting mechanism.
But Comparator allows sorting based on multiple parameters. We can define another class which will implement Comparator interface and then we can override it’s compare(Obj, Obj) method.
Suppose we want to sort the Employee list based on name and salary.

NameComparator.java :
```java
import java.util.Comparator;
public class NameComparator implements Comparator<Employee> {

	@Override
	public int compare(Employee emp1, Employee emp2) {
		return emp1.getName().compareTo(emp2.getName());
	}
}

```

String class already implements Comparable interface and provides a lexicographic implementation for compareTo() method which compares 2 strings based on contents of characters or you can say in lexical order. Here, Java will determine whether passed String object is less than, equal to or greater than the current object.

ComparatorDemo.java :

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ComparatorDemo {
	public static void main(String[] args) {
		List<Employee> empList = new ArrayList<>();
		
		empList.add(new Employee(4, "Dave", 25, 28000));
		empList.add(new Employee(20, "Mike", 20, 10000));
		empList.add(new Employee(9, "Abhi", 32, 5000));
		empList.add(new Employee(1, "Lisa", 40, 19000));
		
		Collections.sort(empList, new NameComparator());
		System.out.println(empList);
	}
}
```

Output:

```log
[Employee [id=9, name=Abhi, age=32, salary=5000]
, Employee [id=4, name=Dave, age=25, salary=28000]
, Employee [id=1, name=Lisa, age=40, salary=19000]
, Employee [id=20, name=Mike, age=20, salary=10000]
]
```

The output list is sorted based on employee’s names.

SalaryComparator.java :
```java
import java.util.Comparator;
public class SalaryComparator implements Comparator<Employee> {
	@Override
	public int compare(Employee emp1, Employee emp2) {
		return (int) (emp1.getSalary() - emp2.getSalary());
	}
}
```
ComparatorDemo.java :
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
public class ComparatorDemo {
	public static void main(String[] args) {
		List<Employee> empList = new ArrayList<>();
		
		empList.add(new Employee(4, "Dave", 25, 28000));
		empList.add(new Employee(20, "Mike", 20, 10000));
		empList.add(new Employee(9, "Abhi", 32, 5000));
		empList.add(new Employee(1, "Lisa", 40, 19000));
		
		Collections.sort(empList, new SalaryComparator());
		System.out.println(empList);
	}
}
```

Output:
```log
[Employee [id=9, name=Abhi, age=32, salary=5000]
, Employee [id=20, name=Mike, age=20, salary=10000]
, Employee [id=1, name=Lisa, age=40, salary=19000]
, Employee [id=4, name=Dave, age=25, salary=28000]
]

```

Comparable and Comparator
-------------------------
- `Comparable` interface can be used to provide single way of sorting whereas `Comparator` interface is used to provide multiple ways of sorting
- `Comparable` interface is present in ‘java.lang’ package whereas `Comparator` interface is present in `java.util` package
- For using `Comparable`, the class needs to implement `Comparable` interface whereas for using `Comparator`, there is no need to make changes in the class
- `Comparable` provides `compareTo()` method to sort elements, whereas `Comparator` provides `compare()` method to sort elements
- We can sort the list elements of `Comparable` type by using `Collections.sort(listObj)` method, whereas to sort the list elements of `Comparator` type, we have to provide a `Comparator` object like, `Collections.sort(listObj, Comparator)`

At times, when you are using any third-party classes or the classes where you are not the author of the class, then in that case `Comparator` is the only choice to sort those objects

static keyword
--------------
In Java, a static member is a member of a class that isn’t associated with an instance of a class. Instead, the member belongs to the class itself.

In Java, Static is applicable for the following:
1.  Variable
2.  Method
3.  Block
4.  Nested class

- **Static Variable** : if any variable is declared as static, then it is known as ‘static variable’. Only single copy of the variable gets created and all instances of the class share same static variable. The static variable gets memory only once in the class area at the time of class loading.
When to use static variable : static variables should be used to declare common property of all objects as only single copy is created and shared among all class objects, for example, the company name of employees etc.

- **Static Method** : When a method is declared with static keyword then it is known as static method. These methods belong to the class rather than the object of the class. As a result, a static method can be directly accessed using class name without the need of creating an object.
One of the basic rules of working with static methods is that you can’t access a non-static method or field from a static method because the static method doesn’t have an instance of the class to use to reference instance methods or fields. Another restriction is, ‘this’ and ‘super’ cannot be used in static context.
For example: main() method is static, Java Runtime uses this method to start an application without creating an object.

- **Static Block** : Static block gets executed exactly once when the class is first loaded, use static block to initialize the static variables.

- **Static nested classes** :
Static nested classes are a type of inner class in java where the inner class is static. Static nested classes can access only the static members of the outer class. The advantage of using static nested classes is that it makes the code more readable and maintainable.
In the case of normal inner class, you cannot create inner class object without first creating the outer class object, but in the case of static inner class, there can be a static inner class object without the outer class object.

How to create object of static inner class:
```java
    OuterClass.StaticNestedClass nestedClassObject = new OuterClass.StaticNestedClass();
```

Compile Time Error comes when we try to access non-static member inside static nested class:

```java

class OuterClass {
    int a = 10;
    static int b = 20;
    private static int c = 30;

    static class InnerClass {
        void print() {
            System.out.println("Outer class variable a : " + a);
            System.out.println("Outer class variable b : " + b);
            System.out.println("Outer class variable c : " + c);
        }
    }
}
    

```
Compile Time Error
```log
Non-static field 'a' cannot be referenced from a static context

```

```java


class OuterClass {
    int a = 10;
    static int b = 20;
    private static int c = 30;

    static class InnerClass {
        void print() {
            //System.out.println("Outer class variable a : " + a);
            System.out.println("Outer class variable b : " + b);
            System.out.println("Outer class variable c : " + c);
        }
    }
}

public class StaticNestedTestClass {
    public static void main(String[] args) {
        OuterClass.InnerClass innerClassObject = new OuterClass.InnerClass();
        innerClassObject.print();
    }
}

```

Output:
```log
Outer class variable b : 20
Outer class variable c : 30
```

If you have static members in your Static Inner class then there is no need to create the inner class object:
```java

class OuterClass {
	static int x = 20;
	
	static class InnerClass {
		static int y = 30;
		
		static void display() {
			System.out.println("Outer x : " + x);
		}
	}
}

public class StaticNestedTestClass {
	public static void main(String[] args) {
		OuterClass.InnerClass.display();
		System.out.println(OuterClass.InnerClass.y);
	}	
}

```

Output: 
```log
Outer x : 20
30
```


Shallow Copy and Deep Copy
-------------------

- **Shallow Copy** : When we use the default implementation of clone() method, a shallow copy of object is returned, meaning if the object that we are trying to clone contains both primitive variables and non-primitive or reference type variable, then only the object’s reference is copied not the entire object itself.

Consider this with the example:
Employee object is having Company object as a reference, now when we perform cloning on Employee object, then for primitive type variables, cloning will be done i.e. new instances will be created and copied to the cloned object but for non-primitive i.e. Company object, only the object’s reference will be copied to the cloned object. It simply means Company object will be same in both original and cloned object, changing the value in one will change the value in other and vice-versa.
Now, if you want to clone the Company object also, so that your original and cloned Employee object will be independent of each other, then you have to perform Deep Copy.

- **Deep Copy** :
In Deep copy, the non-primitive types are also cloned to make the original and cloned object fully independent of each other.

Program 1:

```java

class Company implements Cloneable {
	private String name;
	public Company(String name) {
		this.name = name;
	}
	public String getName() {	return name;	}
	public void setName(String name) {	this.name = name;	}

	@Override
	protected Object clone() throws CloneNotSupportedException {
		return super.clone();
	}
}

public class Employee implements Cloneable {
	private String name;
	private int age;
	private Company company;
	
	public Employee(String name, int age, Company company) {
		this.name = name;
		this.age = age;
		this.company = company;
	}
	
	public String getName() {	return name;	}
	public int getAge() {	return age;		}
	public void setName(String name) {	this.name = name; 	}
	public void setAge(int age) {	this.age = age;		}
	public Company getCompany() {	return company;		}
	public void setCompany(Company company) {	this.company = company;		}

	@Override
	protected Object clone() throws CloneNotSupportedException {
		Employee employee = (Employee) super.clone();
		employee.company = (Company) company.clone();
		return employee;
	}
	public static void main(String[] args) throws CloneNotSupportedException {
		Company c1 = new Company("Company_ABC");
		Employee e1 = new Employee("Mike", 10, c1);
		System.out.println("Employee 1, company name : " + e1.getCompany().getName());
		
		Employee e2 = (Employee) e1.clone();
		System.out.println("Employee 2, company name : " + e2.getCompany().getName());
		e2.getCompany().setName("XYZ");
		System.out.println("----------------------------");
		System.out.println("Employee 1, company name : " + e1.getCompany().getName());
		System.out.println("Employee 2, company name : " + e2.getCompany().getName());
	}
}

```

Output:
```log
Employee 1, company name : Company_ABC
Employee 2, company name : Company_ABC
----------------------------
Employee 1, company name : Company_ABC
Employee 2, company name : XYZ
```

In above example, we have overridden the clone method in our employee class and we called the clone method on mutable company object.


We can also use Copy constructor to perform deep copy:


Program 2:
```java

class Company {
	private String name;
	public Company(String name) {
		this.name = name;
	}
	public String getName() {	return name;	}
	public void setName(String name) {	this.name = name;	}

}

public class Employee {
	private String name;
	private int age;
	private Company company;
	
	public Employee(String name, int age, Company company) {
		this.name = name;
		this.age = age;
		this.company = company;
	}
	
	//Copy constructor
	public Employee(Employee emp) {
		this.name = emp.getName();
		this.age = emp.getAge();
		Company company = new Company(emp.getCompany().getName());
		this.company = company;
	}
	
	public String getName() {	return name;	}
	public int getAge() {	return age;		}
	public void setName(String name) {	this.name = name; 	}
	public void setAge(int age) {	this.age = age;		}
	public Company getCompany() {	return company;		}
	public void setCompany(Company company) {	this.company = company;		}

	public static void main(String[] args) {
		Company c1 = new Company("Company_ABC");
		Employee e1 = new Employee("Mike", 10, c1);
		System.out.println("Employee 1, company name : " + e1.getCompany().getName());
		
		//Invoking copy constructor
		Employee e2 = new Employee(e1);
		System.out.println("Employee 2, company name : " + e2.getCompany().getName());
		e2.getCompany().setName("XYZ");
		System.out.println("----------------------------");
		System.out.println("Employee 1, company name : " + e1.getCompany().getName());
		System.out.println("Employee 2, company name : " + e2.getCompany().getName());
	}
}
```

Output:
```log
Employee 1, company name : Company_ABC
Employee 2, company name : Company_ABC
----------------------------
Employee 1, company name : Company_ABC
Employee 2, company name : XYZ
```

There are 2 other methods by which you can perform deep copy:
- By using Serialization, where you serialize the original object and returns the deserialized object as a clone
- By using external library of Apache Commons Lang. Apache Common Lang comes with SerializationUtils.clone() method for performing deep copy on an object. It expects all classes in the hierarchy to implement Serializable interfaces else SerializableException is thrown by the system



Serialization and De-serialization
-----------------------------------


Serialization is a mechanism to convert the state of an object into a byte stream while De-serialization is the reverse process where the byte stream is used to recreate the actual object in memory. The byte stream created is platform independent that means objects serialized on one platform can be deserialized on another platform.
To make a Java Object serializable, the class must implement Serializable interface. Serializable is a Marker interface. Object

OutputStream and ObjectInputStream classes are used for Serialization and Deserialization in java.
We will serialize the below Employee class:

```java

import java.io.Serializable;

public class Employee implements Serializable{
	private String name;
	private int age;
	private transient int salary;
	
	public Employee(String name, int age, int salary) {
		this.name = name;
		this.age = age;
		this.salary = salary;
	}

	@Override
	public String toString() {
		return "Employee [name=" + name + ", age=" + age + ", salary=" + salary + "]";
	}
	
}


```


SerializationDemo.java:
```java

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

public class SerializationDemo {
	public static void main(String[] args) {
		Employee emp = new Employee("Mike", 15, 20000);
		String file = "byteStream.txt";
		try {
			FileOutputStream fos = new FileOutputStream(file);
			ObjectOutputStream oos = new ObjectOutputStream(fos);			
			oos.writeObject(emp);

			fos.close();
			oos.close();			
			System.out.println("Employee object is serialized : " + emp);
		} catch (IOException e1) {
			System.out.println("IOException is caught");
		}	
		try {
			FileInputStream fis = new FileInputStream(file);
			ObjectInputStream ois = new ObjectInputStream(fis);
			Employee emp1 = (Employee) ois.readObject();
			
			fis.close();
			ois.close();
			System.out.println("Employee object is de-serialized : " + emp1);
		} catch (IOException e) {
			System.out.println("IOException is caught");
		} catch (ClassNotFoundException e) {
			System.out.println("ClassNotFoundException is caught"); 
		}
	}
}


```


Output:
```log
Employee object is serialized : Employee [name=Mike, age=15, salary=20000]
Employee object is de-serialized : Employee [name=Mike, age=15, salary=0]

```

Here, while de-serializing the employee object, salary is 0, that is because we have made salary variable to be ‘transient’. ‘static’ and ‘transient’ variables do not take part in Serialization process. During de-serialization, transient variables will be initialized with their default values i.e. if objects, it will be null and if “int”, it will be 0 and static variables will be having the current value.
And if you look at the file present in current directory bytestream.txt, you can see how the object is serialized into this file,

See file [bytestream.txt](https://github.com/sunilsoni/interview-notes/blob/main/Java/images/byteStream.txt)

