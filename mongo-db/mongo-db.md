MongoDB 
=================

Wikipedia describes as
> MongoDB is a source-available cross-platform document-oriented database program. Classified as a NoSQL database program, MongoDB uses JSON-like documents with optional schemas. MongoDB is developed by MongoDB Inc. and licensed under the Server Side Public License (SSPL).

- MongoDB is an open-source NoSQL database written in C++ language. It uses JSON-like documents with optional schemas. 
- It provides easy scalability and is a cross-platform, document-oriented database.
- MongoDB works on the concept of Collection and Document.
- It combines the ability to scale out with features such as secondary indexes, range queries, sorting, aggregations, and geospatial indexes.
- MongoDB is developed by MongoDB Inc. and licensed under the Server Side Public License (SSPL).


MongoDB is a document-based database created in 2007 by 10gen software. It works on the concept of collections and documents. A MongoDB server can contain multiple databases and offers high performance along with redundancy and easy scalability. Collection in MongoDB can be considered as a group of documents that can have different types of fields. The document is a set of key-value pairs having a dynamic schema i.e. common fields may hold different types of data and all documents in the same collection need not have the same structure. If you are new to MongoDB but have worked with RDBMS like SQL before, this small table will help you correlate the terminologies:

|  RDBMS  | MongoDB  |
| ----------- | ----------- |
|   Table    |   Collection   |
|   Row    |   Document   |
|   Column    |   Field   |
|   Table join    |  Embedded documents |

Key Components
--------------
1. **_id**: The _id field represents a unique value in the MongoDB document. The _id field is like the document's primary key. If you create a new document without an _id field, MongoDB will automatically create the field.
2. **Collection**: This is a grouping of MongoDB documents. A collection is the equivalent of a table which is created in any other RDMS such as Oracle.
3. **Cursor**: This is a pointer to the result set of a query. Clients can iterate through a cursor to retrieve results.
4. **Database**: This is a container for collections like in RDMS wherein it is a container for tables. Each database gets its own set of files on the file system. A MongoDB server can store multiple databases.
5. **Document**: A record in a MongoDB collection is basically called a document. The document, in turn, will consist of field name and values.
6. **Field**: A name-value pair in a document. A document has zero or more fields. Fields are analogous to columns in relational databases.

Document
----------
A Document in MongoDB is an ordered set of keys with associated values. It is represented by a map, hash, or dictionary. In JavaScript, documents are represented as objects:
```json
{"greeting" : "Hello world!"}
```
Complex documents will contain multiple key/value pairs:
```json
{"greeting" : "Hello world!", "views" : 3}
```

Collection
----------

A collection in MongoDB is a group of documents. If a document is the MongoDB analog of a row in a relational database, then a collection can be thought of as the analog to a table.
Documents within a single collection can have any number of different “shapes.”, i.e. collections have dynamic schemas.

For example, both of the following documents could be stored in a single collection:
```json
{"greeting" : "Hello world!", "views": 3}
{"signoff": "Good bye"}
```

Namespace
----------

MongoDB stores BSON (Binary Interchange and Structure Object Notation) objects in the collection. The concatenation of the collection name and database name is called a namespace



Databases in MongoDB
----------
MongoDB groups collections into databases. MongoDB can host several databases, each grouping together collections.
Some reserved database names are as follows:
```
  admin
  local
  config
```

Mongo Shell
----------
It is a JavaScript shell that allows interaction with a MongoDB instance from the command line. With that one can perform administrative functions, inspecting an instance, or exploring MongoDB.

To start the shell, run the mongo executable:
```shell
$ mongod
$ mongo
MongoDB shell version: 4.2.0
connecting to: test
>
```

The shell is a full-featured JavaScript interpreter, capable of running arbitrary JavaScript programs. Let’s see how basic math works on this:
```shell
> x = 100;
200
> x / 5;
20
```

Advantages of MongoDB:
--------------

Some advantages of MongoDB are as follows:

- Cross-platform
- Written in C++.
- Secure and scalable
- Schema-less database
- Document-oriented
- Supports high-availability and redundancy
- MongoDB supports field, range-based, string pattern matching type queries. for searching the data in the database
- MongoDB support primary and secondary index on any fields
- MongoDB basically uses JavaScript objects in place of procedures
- MongoDB uses a dynamic database schema
- MongoDB is very easy to scale up or down
- MongoDB has inbuilt support for data partitioning (Sharding).


Features of MongoDB
--------------

Feature  | Description  |
| ----------- | ----------- |
|   Indexing    |   It indexes are created in order to improve the search performance.   |
|   Replication    |   MongoDB distributes the data across different machines.   |
|   Ad-hoc Queries    |   It supports ad-hoc queries by indexing the BSON documents & using a unique query language.   |
|   Schemaless   |  It is very flexible because of its schema-less database that is written in C++. |
|   Sharding   |  MongoDB uses sharding to enable deployments with very large data sets and high throughput operations. |

Indexes in MongoDB
--------------
MongoDB supports the following types of the index for running a query.
1. Single Field Index
2. Compound Index
3. Multikey Index
4. Geospatial Index
5. Text Index
6. Hashed Index








For more information:
1. [MongoDB Interview Questions and Answers](https://hackr.io/blog/mongodb-interview-questions)
2. [MongoDB Interview Questions](https://www.interviewbit.com/mongodb-interview-questions/)
3. [MongoDB Interview Questions For Beginners And Professionals In 2020](https://www.edureka.co/blog/mongodb-interview-questions-for-beginners-and-professionals)