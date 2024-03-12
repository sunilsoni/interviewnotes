Spring Transaction Management:
=================
> A transaction is a logical unit of work that either completely succeeds or fails. Think about a banking transaction. Here, the unit of work is money debiting from Account A and money crediting to Account B. If one of them fails, the entire process fails. We call it a rollback of all the steps in the transaction if anything fails in between.


Global Transactions
--------------------
There can be applications (very unlikely) where the transaction can happen between different databases. This is called distributed transaction processing. The transaction manager cannot sit within the application to handle it, rather it sits in the application server level. JTA or java transaction API is required with the support of JNDI to lookup different databases, and the transaction manager decides the commit or rollback of the distributed transaction. This is a complex process and requires knowledge at the application server level.

Local Transactions
--------------------
Local transactions happen between the application and a singled RDBMS, such as a simple JDBC connection. With local transaction, all the transaction code is within our code.

In both global and local transaction, we have to manage the transaction by ourselves. If I am using JDBC, then the transaction management API is for JDBC. If I am using Hibernate, then the hibernate transaction API and JTA at application server is for global transactions.


Spring framework overcomes all of the these problems by providing an abstraction over the different transaction APIs, providing a consistent programming model. The abstraction is via org.springframework.transaction.PlatformTransactionManager interface. Here is the snippet of the interface:

```java
public interface PlatformTransactionManager {
    TransactionStatus getTransaction(TransactionDefinition definition) throws TransactionException;

    void commit(TransactionStatus status) throws TransactionException;

    void rollback(TransactionStatus status) throws TransactionException;
}
```
There are various spring managed transaction managers that implement PlatformTransactionManager. Some of them are:

- **org.springframework.orm.jpa.JpaTransactionManager** — For JPA transactions
- **org.springframework.jdbc.datasource.DataSourceTransactionManager** — For JDBC transactions
- **org.springframework.orm.hibernate5.HibernateTransactionManager** — For Hibernate transactions and it binds with SessionFactory
- **org.springframework.transaction.jta.JtaTransactionManager** — For JTA transactions.
- **org.springframework.transaction.jta.WebLogicJtaTransactionManager** — For Oracle Weblogic managed transaction
- **org.springframework.transaction.jta.WebSphereUowTransactionManager** — For IBM Websphere Application Server managed transactions.
- **org.springframework.jms.connection.JmsTransactionManager** — For JMS messaging transaction by binding JMS connection factory.

Spring transactions can be managed by 2 approaches: programmatic and declarative.

Programmatic Approach:
--------------------
Spring provides a programmatic approach in 2 ways :

1. Using the TransactionTemplate
2. Using a `PlatformTransactionManager` implementation directly

The programmatic approach is not widely used, as the transaction management sits with the business logic. In an application where we have transactions for a few CRUD operations, the programmatic approach is preferred as transaction proxies can be a heavy operation.


Declarative Approach (@Transactional)
--------------------
The declarative approach is widely used because transaction management stays out of business logic. It uses AOP proxies behind to drive transactions around method invocation with appropriate TransactionManager. It can be done either with annotation or with XML. But nowadays, most of the applications are annotation based, so I am covering how it works with the annotations.


- **1. Use `@EnableTransactionManagement`** at the top of the configuration class, which has `@Configuration` annotation. This is the same as the XML tag:

```xml
 <tx:annotation-driven transaction-manager="txManager"/>
```

```java
@Configuration
@EnableTransactionmanagement
public class SpringConfiguration{
...........
        ...........
} 
```

- **2. Define the datasource and transaction manager**

```java
    @Bean
     public FooRepository fooRepository() {
         // configure and return a class having @Transactional methods
         return new JdbcFooRepository(dataSource());
     }

     @Bean
     public DataSource dataSource() {
         // configure and return the necessary JDBC DataSource
     }

     @Bean
     public PlatformTransactionManager txManager() {
         return new DataSourceTransactionManager(dataSource());
     }
} 
```

- **3. Use the @Transactional annotation** above the methods and concrete classes. If applied at class level, all the methods will be by default transactional.

Let's try to understand how the annotation works with a simple example:

Assume we have a sample service lass

```java
 Class SampleService {
    @Transactional
    public void serviceMethod(){
        //call to dao layer 
    }
}
```

When SampleService is injected in another class, Spring will inject it in the below manner internally:

```java
 class ProxySampleService extends SampleService{
    private SampleService sampleService;
    public ProxySampleService(SampleService s){
        this.sampleService=s;
    }
    @Override
    public void sampleMethod(){
        try{
            //open transaction 
            sampleService.sampleMethod();
            //close transaction
        }
        catch(Exception e){
            //rollback
        }

    }

}
```

This is the proxy design that works behind the scenes.

Now let's see how we can fine tune the @Transactional annotation by changing the setting of the attributes.

Settings of the attributes in @Transactional annotation:

propagation
-----------
Optional setting for propagation. This is a very important attribute in setting the transactional behavior. I will cover a use case of it below.
- **REQUIRED** — support a current transaction, create a new one if none exist
- **REQUIRES_NEW** — create a new transaction and suspend the current transaction if none exist
- **MANDATORY** — support a current transaction, throw an exception if none exists
- **NESTED** — executes within a nested transaction if a current transaction exists
- **SUPPORTS** — supports currents transaction but execute non-transactionally if none exists

isolation
-----------
transaction isolation level. It decides the level to what the transaction should be isolated to other transactions
- **DEFAULT** — default isolation level of the datasource
- **READ_COMMITTED** — indicates dirty reads to be prevented, non-repeatable, and phantom reads can occur.
- **READ_UNCOMMITTED** — indicates that dirty reads, non-repeatable, and phantom reads can occur
- **REPEATABLE_READ** — indicates dirty and non-repeatable reads are prevented but phantom reads can occur
- **SERIALIZABLE** — indicates dirty read phantom read, and non-repeatable reads are prevented


we also have  other settings

- **readOnly** whether the transaction is read-only or read/write
- **timeout** — transaction timeout
- **rollbackFor** — arrays of exception class objects that must cause a rollback of the transaction
- **rollbackForClassName** — arrays of exception class names that must cause a rollback of the transaction
- **noRollbackFor** — arrays of exception class objects that must not cause a rollback of the transaction
- **noRollbackForClassName** — arrays of exception class names that must not cause a rollback of the transaction

```java
 
```

For more information:

1. [Spring Transactional Management](https://dzone.com/articles/bountyspring-transactional-management)