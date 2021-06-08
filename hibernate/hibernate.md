Hibernate
=================

Hibernate is an Object Relational Mapping tool (ORM tool), that maps the Java objects to the database tables and vice-versa.

Some points to remember:
- Hibernate framework provides the facility to create database tables automatically
- Hibernate framework provides us object-oriented version of SQL known as HQL (Hibernate Query Language). It generates the database independent queries. So, even if our database gets changed, we don’t have to change our SQL queries according to the new database
- Using Hibernate, we can define relationships between our Entities (tables), that makes it easy to fetch data from multiple tables
- Hibernate supports Caching, that improves the performance of our application
- Using Hibernate, we can generate the Primary key of our tables automatically


JPA vs Hibernate
-----------------
JPA is just a specification i.e. it defines a set of concepts that can be implemented by any tool or framework, and Hibernate is one of the implementation of JPA.


@Entity annotation
------------------
@Entity annotation defines that a class can be mapped to a database table. The class fields will be mapped to the columns of the table.


@Id & @GeneratedValue
------------------
@Id annotation defines the primary key of a table and @GeneratedValue annotation is used to specify the primary key generation strategy to use. If the strategy is not specified, the default strategy AUTO will be used.

get() and load() methods of Hibernate Session
------------------

Hibernate Session class provides two methods to access object, session.get() and session.load()

The differences are:
- get() method involves a database hit, if the object does not exist in Session cache and it returns a fully initialized object which may involve several database calls, whereas load() method returns a proxy object and it only hit the database if any method other than getId() is called on the entity object
- load() method results in slightly better performance as it can return a proxy object, it will only hit the database when a non-identifier getter method is called, whereas get() method returns a fully initialized object when it does not exist in Session cache which may involve multiple database calls based on entity relationships
- get() method returns null if the object is not found in the cache as well as the database whereas load() method will throw ObjectNotFoundException but never return null
- If you are not sure whether the object exists or not, then use get() as it will return null but if you are sure that the object exists, then use load() method as it is lazily initialized


save(), saveOrUpdate() and persist() method of Hibernate Session
------------------
Hibernate Session class provides various methods to save an object into the database, like save(), saveOrUpdate() and persist()

The difference between save() and saveOrUpdate() method is that save() method saves the record into the database by INSERT query, generates a new identifier and returns the Serializable identifier back, while saveOrUpdate() method either INSERT the record or UPDATE the record if it already exists, so it involves extra processing to find whether the record already exists in the table or not.
Similar to save(), persist() method is also used to save the record into the database table.

The differences between save() and persist() are:

- Return type of persist() method is void while return type of save() method is Serializable object
- Both persist() and save() methods makes a transient instance persistent. But persist() method does not guarantee that the identifier value will be assigned to the persistent instance immediately, the assignment might happen at flush time
- Both behave differently when they are executed outside the transaction boundaries. persist() method ensures that it will not execute an INSERT when it is called outside of a transaction boundary whereas save() method does not guarantee this, it returns an identifier and if an INSERT query has to be executed to get the identifier then this INSERT happens immediately and it does not matter if the save() is called inside or outside of a transaction
-  persist() method is useful in long-running conversation with an extended Session context because it does not execute an INSERT outside of a transaction. On the other hand, save() method is not good in a long-running conversation with an extended Session context

