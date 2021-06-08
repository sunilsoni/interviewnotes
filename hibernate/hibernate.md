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


Session and SessionFactory
------------------
SessionFactory creates and manages the Session objects.

**Some points about SessionFactory:**
- it is one instance per datasource/database
- it is thread-safe
- it is an immutable and heavy-weight object as it maintains Sessions, mappings, hibernate configurations etc.
- SessionFactory provides second level cache in hibernate also called application-level cache

**Some points about Session:**
- Session objects are created using sessionFactory.openSession()
- It is one instance per client/thread/transaction
- It is not thread-safe
- It is light-weight
- Session provides first level cache, which is short-lived

First Level and Second Level Cache
------------------
Hibernate framework provides caching at two levels, first-level cache which is at the Session level and second-level cache which is at the application level.

**The first level cache** minimizes the database access for the same object if it is requested from the same Session. The first level cache is by default enabled. When you call session.get() method then it hits the database, and while returning, it also saves this object in the first-level cache. So, the subsequent requests for this same object from the same session will not hit the database and the object from cache will be used.

But, since this cache is associated with the Session object, which is a short-lived object in Hibernate, as soon as the session is closed, all the information held in the cache is also lost. So, if we try to load the same object using the get() method, Hibernate will go to the database again and fetch the record.

This poses a significant performance challenge in an application where multiple sessions are used, Hibernate provides second-level cache for this and it can be shared among multiple sessions.

**The second level cache** is maintained at the SessionFactory level, this cache is by default disabled, to enable second level cache in hibernate, it needs to be configured in hibernate configuration file, i.e. hibernate.cfg.xml file. There are various providers of second level cache, like EhCache, OSCache etc.

Once second level cache is configured, then object request will first go to the first-level cache, if it is not found there, then it will look for this object in second-level cache, if found then it will be returned from the second-level cache and it will also save a copy in first-level cache.

But, If the object is not found in the second-level cache also, then it will hit the database and if it present in database, this object will be put into both first and second level cache, so that if any other session requests for this object then it will be returned from the cache.




