Collection Framework
====================

Collection framework represents an architecture to store and manipulate a group of objects. All the classes and interfaces of this framework are present in java.util package.

Some points:
- Iterable interface is the root interface for all collection classes, it has one abstract method iterator()
- Collection interface extends the Iterable interface


HashMap
-------

HashMap class implements the Map interface and it stores data in key, value pairs. HashMap provides constant time performance for its get() and put() operations, assuming the equals and hashcode method has been implemented properly, so that elements can be distributed correctly among the buckets.

Some points to remember:
- Keys should be unique in HashMap, if you try to insert the duplicate key, then it will override the corresponding key’s value
- HashMap may have one null key and multiple null values
- HashMap does not guarantee the insertion order (if you want to maintain the insertion order, use LinkedHashMap class)
- HashMap is not synchronized
- HashMap uses an inner class Node<K, V> for storing map entries
- Hashmap has a default initial capacity of 16, which means it has 16 buckets or bins to store map entries, each bucket is a singly linked list. The default load factor in HashMap is 0.75
- Load factor is that threshold value which when crossed will double the hashmap’s capacity i.e. when you add 13th element in hashmap, the capacity will increase from 16 to 32


Interal working of put() and get() methods of HashMap :
-----------------------------------

- **put() method internal working**:
When you call map.put(key,value), the below things happens:
  
- Key’s hashCode() method is called
- Hashmap has an internal hash function which takes the key’s hashCode and it calculates the bucket index
- If there is no element present at that bucket index, our <key, value> pair along with hash is stored at that bucket
- But if there is an element present at the bucket index, then key’s hashCode is used to check whether this key is already present with the same hashCode or not.

If there is key with same hashCode, then equals method is used on the key. If equals method returns true, then the key’s previous value is replaced with the new value otherwise a new entry is appended to the linked list.


- **get() method internal working**:
  When you call map.get(key), the below things happen:
  
- Key’s hashCode() method is called
- Hash function uses this hashCode to calculate the index, just like in put method
- Now the key of element stored in bucket is compared with the passed key using equals() method, if both are equals, value is returned otherwise the next element is checked if it exists.

See HashMap’s Javadoc:
Default capacity:
```java
/**
* The default initial capacity - MUST be a power of two.
*/
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16
```

Load factor:
```java
/**
* The load factor used when none specified in constructor.
*/
static final float DEFAULT_LOAD_FACTOR = 0.75f;
```

Node class:
```java
static class Node<K,V> implements Map.Entry<K,V> {
final int hash ;
“final K key ;
    V value ;
    Node<K,V> next ;
    Node(int hash , K key , V value , Node<K,V> next ) {
        this .hash = hash ;
        this .key = key ;
        this .value = value ;
        this .next = next ;
    }
```

Internal Hash function:

```java
static final int hash(Object key ) {
int h ;
return (key == null ) ? 0 : (h = key .hashCode()) ^ (h >>> 16);
}
```

Internal Data structure used by HashMap to hold buckets:
```java
transient Node<K,V>[] table ;

```

HashMap’s default constructor:

```java
/**
* Constructs an empty <tt> HashMap </tt> with the default initial capacity
* (16) and the default load factor (0.75).
  */
public HashMap() {
this .loadFactor = DEFAULT_LOAD_FACTOR ; // all other fields defaulted
}
```
So, to conclude, Hashmap internally uses an array of Nodes named as table where each Node contains the calculated hash value, the key-value pair and the address to the next node.

HashMap collisions
------------------
It is possible that multiple keys will make the hash function generate the same index, this is called a collision. It happens because of poor hashcode method implementation.

One collision handling technique is called Chaining. Since every element in the array is a linked list, the keys which have the same hash function will be appended to the linked list.

- **Performance improvement in Java 8** : 
  It is possible that due to multiple collisions, the linked list size has become very large, and as we know, searching in a linked list is O(n), it will impact the constant time performance of hashmap’s get() method. So, in Java 8, if the linked list size becomes more than 8, the linked list is converted to a binary search tree which will give a better time complexity of O(log n).
```java
/**
* The bin count threshold for using a tree rather than list for a
* bin. Bins are converted to trees when adding an element to a”
 “* bin with at least this many nodes. The value must be greater
 * than 2 and should be at least 8 to mesh with assumptions in
 * tree removal about conversion back to plain bins upon
 * shrinkage.
 */
static final int TREEIFY_THRESHOLD = 8;

```
Program showing the default capacity:
```java
import java.lang.reflect.Field;
import java.util.HashMap;

public class TestHashMap {
    public static void main(String[] args) throws Exception {
        HashMap<String, String> map = new HashMap<>();
        map.put("name", "Mike");

		Field tableField = HashMap.class.getDeclaredField("table");
		tableField.setAccessible(true);
		Object[] table = (Object[]) tableField.get(map);
		System.out.print("hashmap capacity: ");
		System.out.print(table == null ? 0 : table.length);
		System.out.println("\nhashmap size:" + map.size());
	}
}
```

Output:
```log
hashmap capacity: 16
hashmap size: 1
```
Program showing that hashmap’s capacity gets doubled after load factor’s threshold value breaches :

```java

import java.lang.reflect.Field;
import java.util.HashMap;

class Employee {
	private int age;
	
	public Employee(int age) {
		this.age = age;
	}
}

public class TestHashMap {
	public static void main(String[] args) throws Exception {
		HashMap<Employee, String> map = new HashMap<>();
		
		for(int i=1;i<13;i++) {
			map.put(new Employee(i), "Hello " + i);
		}
		
		Field tableField = HashMap.class.getDeclaredField("table");
		tableField.setAccessible(true);
		Object[] table = (Object[]) tableField.get(map);
		System.out.print("hashmap capacity: ");
		System.out.print(table == null ? 0 : table.length);
		System.out.println("\nhashmap size:" + map.size());
	}
}

```

Output:
```log
hashmap capacity: 16
hashmap size: 12
```

Change the for loop condition from i<13 to i<=13, see below:


```java

import java.lang.reflect.Field;
import java.util.HashMap;

class Employee {
	private int age;
	
	public Employee(int age) {
		this.age = age;
	}
}

public class TestHashMap {
	public static void main(String[] args) throws Exception {
		HashMap<Employee, String> map = new HashMap<>();
		
		for(int i=1;i<13;i++) {
			map.put(new Employee(i), "Hello " + i);
		}
		
		Field tableField = HashMap.class.getDeclaredField("table");
		tableField.setAccessible(true);
		Object[] table = (Object[]) tableField.get(map);
		System.out.print("hashmap capacity: ");
		System.out.print(table == null ? 0 : table.length);
		System.out.println("\nhashmap size:" + map.size());
	}
}

```

Output:
```log
hashmap capacity: 32
hashmap size: 13
```

equals and hashCode method in HashMap when the key is a custom class
-----------------

`equals` and `hashCode` methods are called when we store and retrieve values from hashmap.

if in your custom class, you are not implementing `equals()` and `hashCode()`, then the Object class `equals()` and `hashCode()` will be called, and the contract between these 2 methods. 
It says when 2 objects are equal according to equals() method, then their hashCode must be same, reverse may not be true.

- **Scenario 1**: when custom class does not implement both equals and hashCode methods
```java
public class Employee {
  private String name;
  private int age;
  public Employee(String name, int age) {
    this.name = name;
    this.age = age;
  }
}
```
Here, `Employee` class has not given `equals()` and `hashCode()` method implementation, so Object’s class `equals()` and `hashCode()` methods will be used when we use this `Employee` class as hashmap’s key, and remember, equals() method of Object class compares the reference.

TestHashMap.java:
```java

import java.util.HashMap;
import java.util.Map;

public class TestHashMap {
  public static void main(String[] args) {

    Map<Employee, Integer> map = new HashMap<>();

    Employee e1 = new Employee("Mike", 15);
    Employee e2 = new Employee("Mike", 15);
    Employee e3 = new Employee("John", 20);
    Employee e4 = e3;

    System.out.println("e1 hashcode: " + e1.hashCode());
    System.out.println("e2 hashcode: " + e2.hashCode());
    System.out.println("e3 hashcode: " + e3.hashCode());
    System.out.println("e4 hashcode: " + e4.hashCode());

    System.out.println("e1 equals e2: " + e1.equals(e2));
    System.out.println("e3 equals e4: " + e3.equals(e4));

    map.put(e1, 100);
    map.put(e2, 200);
    map.put(e3, 300);
    map.put(e4, 400);

    System.out.println(map.get(e1));
    System.out.println(map.get(e2));
    System.out.println(map.get(e3));
    System.out.println(map.get(e4));
    System.out.println("hashmap size: " + map.size());
  }
}
```

Output:
```log
e1 hashcode: 1324119927
e2 hashcode: 999966131
e3 hashcode: 1989780873
e4 hashcode: 1989780873
e1 equals e2: false
e3 equals e4: true
100
200
400
400
hashmap size: 3
```
Here, `Employee` objects e1 and e2 are same but they are both inserted in the `HashMap` because both are created using new keyword and holding a different reference, and as the Object’s `equals()` method checks reference, they both are unique.
And as for objects e3 and e4, they both are pointing to same reference (e4 = e3), so they are equal according to Object’s `equals()` method hence the value of e3 which was 300 gets replaced with the value 400 of the same key e4, and finally size of HashMap is 3.


- **Scenario 2**:  when only equals() method is implemented by Employee class

```java

public class Employee {

  private String name;
  private int age;

  public Employee(String name, int age) {
    this.name = name;
    this.age = age;
  }

  @Override
  public boolean equals(Object obj) {
    if (this == obj)
      return true;
    if (obj == null)
      return false;
    if (getClass() != obj.getClass())
      return false;
    Employee other = (Employee) obj;
    if (age != other.age)
      return false;
    if (name == null) {
      if (other.name != null)
        return false;
    } else if (!name.equals(other.name))
      return false;
    return true;
  }

}
```

```java

import java.util.HashMap;
import java.util.Map;

public class TestHashMap {
  public static void main(String[] args) {

    Map<Employee, Integer> map = new HashMap<>();

    Employee e1 = new Employee("Mike", 15);
    Employee e2 = new Employee("Mike", 15);
    Employee e3 = new Employee("John", 20);
    Employee e4 = e3;

    System.out.println("e1 hashcode: " + e1.hashCode());
    System.out.println("e2 hashcode: " + e2.hashCode());
    System.out.println("e3 hashcode: " + e3.hashCode());
    System.out.println("e4 hashcode: " + e4.hashCode());

    System.out.println("e1 equals e2: " + e1.equals(e2));
    System.out.println("e3 equals e4: " + e3.equals(e4));

    map.put(e1, 100);
    map.put(e2, 200);
    map.put(e3, 300);
    map.put(e4, 400);

    System.out.println(map.get(e1));
    System.out.println(map.get(e2));
    System.out.println(map.get(e3));
    System.out.println(map.get(e4));
    System.out.println("hashmap size: " + map.size());
  }
}
```



Let’s see the output:
```log
e1 hashcode: 1324119927
e2 hashcode: 999966131
e3 hashcode: 1989780873
e4 hashcode: 1989780873
e1 equals e2: true
e3 equals e4: true
100
200
400
400
hashmap size: 3
```

Well, nothing’s changed here. Because even though e1 and e2 are equal according to our newly implemented `equals()` method, they still have different hashCode as the Object’s class `hashCode()` is used. So the equals and hashCode contract is not followed and both e1, e2 got inserted in `HashMap`.

- **Scenario 3**:  when only hashCode() method is implemented:



```java

public class Employee {
  private String name;
  private int age;

  public Employee(String name, int age) {
    this.name = name;
    this.age = age;
  }

  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + age;
    result = prime * result + ((name == null) ? 0 : name.hashCode());
    return result;
  }

}
```


Let’s run our `TestHashMap` class again and see the output: 
```log
e1 hashcode: 2399656
e2 hashcode: 2399656
e3 hashcode: 2316120
e4 hashcode: 2316120
e1 equals e2: false
e3 equals e4: true
100
200
400
400
hashmap size: 3

```

Well, now we have same hashCode for e1 and e2, but Object’s equals method still checks the references and as references are different, both are not equal and are inserted in the hashmap.

- **Scenario 4**: When both equals and hashCode are implemented properly:

```java

public class Employee {
    private String name;
    private int age;

    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + age;
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        return result;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        Employee other = (Employee) obj;
        if (age != other.age)
            return false;
        if (name == null) {
            if (other.name != null)
                return false;
        } else if (!name.equals(other.name))
            return false;
        return true;
    }
}
```

Output:

```log
e1 hashcode: 2399656
e2 hashcode: 2399656
e3 hashcode: 2316120
e4 hashcode: 2316120
e1 equals e2: true
e3 equals e4: true
200
200
400
400
hashmap size: 2
```
Here, both e1 and e2 are equals as we are comparing the contents of them in our `equals()` method, so their hashCodes must be same, which they are. So value of e1 which was 100 got replaced by 200, and size of hashmap is 2.

You can be asked to write the `equals()` and `hashCode()` methods implementation by hand also, so you should pay attention to how these are implemented.


How to make a HashMap synchronized?

Collections.synchronizedMap(map);

Concurrent HashMap
------------------

`ConcurrentHashMap` class provides concurrent access to the map, this class is very similar to `HashTable`, except that `ConcurrentHashMap` provides better concurrency than `HashTable` or even `synchronizedMap`.

Some points to remember:
- `ConcurrentHashMap` is internally divided into segments, by default size is 16 that means, at max 16 threads can work at a time
- Unlike `HashTable`, the entire map is not locked while reading/writing from the map
- In `ConcurrentHashMap`, concurrent threads can read the value without locking
- For adding or updating the map, the lock is obtained on segment level, that means each thread can work on each segment during high concurrency
- Concurrency level defines a number, which is an estimated number of threads concurrently accessing the map
- `ConcurrentHashMap` does not allow null keys or null values
- put() method acquires lock on the segment
- get() method returns the most recently updated value
- iterators returned by `ConcurrentHashMap` are fail-safe and never throw `ConcurrentModificationException`

HashSet class
--------------
HashSet is a class in Java that implements the Set Interface and it allows us to have the unique elements only. HashSet class does not maintain the insertion order of elements, if you want to maintain the insertion order, then you can use LinkedHashSet.

- **Internal implementation of HashSet:**

HashSet internally uses HashMap and as we know the keys are unique in hashmap, the value passed in the add() method of HashSet is stored as the key of hashmap, that is how Set maintains the unique elements.

```java
/**
* Constructs a new, empty set; the backing <tt> HashMap </tt> instance has
* default initial capacity (16) and load factor (0.75).
*/
public HashSet() {
        map = new HashMap<>();
}
private transient HashMap<E,Object> map ;

```
Let’s see add() method’s Javadoc:
```java
public boolean add(E e ) {
        return map .put(e , PRESENT )==null ;
}
// Dummy value to associate with an Object in the backing Map
private static final Object PRESENT = new Object();
```

So, when we call hashSet.add(element) method then
- map.put() is called where key is the element and value is the dummy value (the map.put() method internal working has already been discussed above)
- if value is added in the map then put method will return null which will be compared with null, hence returning true from hashSet.add() method indicating the element is added
- however if the element is already present in the map, then the value associated with the element will be returned which in turn will be compared with null, returning false from hashSet.add() method

set.contains() method:

```java
public boolean contains(Object o ) {
    return map .containsKey(o );
}
```
The passed object is given to map.containsKey() method, as the HashSet’s values are stored as the keys of internal map.

NOTE: If you are adding a custom class object inside the HashSet, do follow equals and hashCode contract.





