# Managing transactions

## ACID Transactions

Typically, when we talk about database transactions, we are talking about ACID transactions.

ACID stands for atomicity, consistency, isolation, and durability, and here is what these properties give us:

**Atomicity**
Ensures that all operations completed within the transaction either all complete or all fail. If any of the changes
we’re trying to make fail for some reason, then the whole operation is aborted, and it’s as though no changes were ever
made.

**Consistency**
When changes are made to our database, we ensure it is left in a valid, consistent state.

**Isolation**
Allows multiple transactions to operate at the same time without interfering. This is achieved by ensuring that any
interim state changes made during one transaction are invisible to other transactions.

**Durability**
Makes sure that once a transaction has been completed, we are confident the data won’t get lost in the event of some
system failure.

## What is a distributed transaction?

When a microservice architecture decomposes a monolithic system into self-encapsulated services, it can break
transactions. This means a local transaction in the monolithic system is now distributed into multiple services that
will be called in a sequence.

Here is a customer order example with a monolithic system using a local transaction:

<img src="./images-ms/monolithic system using a local transactio.png" width="800"/>


In the customer order example above, if a user sends a Put Order action to a monolithic system, the system will create a
local database transaction that works over multiple database tables. If any step fails, the transaction can roll back.
This is known as ACID (Atomicity, Consistency, Isolation, Durability), which is guaranteed by the database system.

When we decompose this system, we created both the `CustomerMicroserviceand` the `OrderMicroservice`, which have
separate databases. Here is a customer order example with microservices:


<img src="./images-ms/customer order example with microservices.png" width="800" />

When a Put Order request comes from the user, both microservices will be called to apply changes into their own
database. Because the transaction is now across multiple databases, it is now considered a _distributed transaction_.

**What is the problem?**
In a monolithic system, we have a database system to ensure ACIDity. We now need to clarify the following key problems.

**How do we keep the transaction atomic?**
In a database system, atomicity means that in a transaction either all steps complete or no steps complete. The
microservice-based system does not have a global transaction coordinator by default. In the example above, if
the `CreateOrder` method fails, how do we roll back the changes we applied by the `CustomerMicroservice`?

**Do we isolate user actions for concurrent requests?**
If an object is written by a transaction and at the same time (before the transaction ends), it is read by another
request, should the object return old data or updated data? In the example above, once UpdateCustomerFund succeeds but
is still waiting for a response from CreateOrder, should requests for the current customer's fund return the updated
amount or not?

**Possible solutions**

The problems above are important for microservice-based systems. Otherwise, there is no way to tell if a transaction has
completed successfully. The following two patterns can resolve the problem:

1. 2pc (two-phase commit)
2. Saga

## Two-phase commit (2pc) pattern

### Benefits of using 2pc

### Disadvantages of using 2pc

## Saga pattern

### Advantages of the Saga pattern

### Disadvantages of the Saga pattern

**Adding a process manager**




