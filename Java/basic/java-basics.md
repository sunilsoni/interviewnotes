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