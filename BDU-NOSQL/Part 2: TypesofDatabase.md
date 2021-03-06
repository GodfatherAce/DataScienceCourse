Defining NoSQL Database Types, Options, and Use Cases Script
==============================================================

This second lesson provides an overview of the types of NoSQL databases.

This lesson defines the four major types of NoSQL databases, including the primary use case, major
architectural differences, advantages, and disadvantages of each type.

There are four major types of NoSQL databases:
* Key-Value
* Document
* Column-Family
* And Graph.

All have unique characteristics that make them great fits for different types of applications or parts of
applications. Let’s move on and dive into each type, speaking to both the architecture and use cases for
each.

#### Key-Value Databases 
Key-Value databases are the least complex of the NoSQL databases. 

All data is stored with a key and an associated value blob. 

Because Key-Value stores are represented as a hashmap, they're powerful for basic
***Create-Read-Update-Delete*** operations, and these databases typically scale quite well and shard easily
across 'x' number of nodes. Each shard would contain a range of keys and their associated values.
However, these databases are usually not meant for complex queries attempting to connect multiple
pieces of data, and are atomic for single key operations only. The value blob is opaque and therefore
typically will have less flexibility when it comes to indexing and querying the data than other database
types.

When would be the best time to incorporate a Key-Value store? Well, anytime you need quick
performance for basic Create-Read-Update-Delete operations and your data is not interconnected.
For example, storing and retrieving session information for a Web application. Each user session would
receive some sort of unique key and all data would be stored together in the opaque value blob. Plus,
there would be no need to query based on the information in the value blob. All transactions would be
based on the unique key.

Similar use cases would be for storing user profiles and preferences within an application or even storing
shopping cart data for online stores or marketplaces. Complex queries or handling relationships between
different keys would be few and far between.

Key-Value stores would not fit use cases that require just the opposite. When there are many-to-many
relationships in the data, a Key-Value store is likely to exhibit poor performance.
Also, if your use case requires a high level of consistency for multi-operation transactions, you may want
to look more towards databases that provide Atomicity, Consistency, Isolation, and Durability, or ACID,
transactions.

Lastly, if you expect the need to query based on value versus key, it may be wise to consider the next type
of NoSQL database we're going to cover, that being a document database.
This screen shows some of the more popular types of key-value databases.

Document databases build off the Key-Value model by making the value visible and able to be queried.
Each piece of data is considered a document and typically stored in either JSON or XML format.

One of the benefits of document databases is that each document truly offers a flexible schema, where no
two documents need to be the same or containing the same information.

Document databases typically offer the ability to index and query the contents of the documents, offering
key and value range lookups and search ability, or perhaps analytical queries via paradigms like
MapReduce.

#### 2. Document Databases

Document databases are horizontally scalable and allow for sharding across multiple nodes, typically
sharded by some unique key in the document. Document stores also typically only guarantee atomic
transactions on single document operations.

What are some use cases for when to use a document database?

* The first example would be for event logging for an application or process. Each instance would constitute
a new document or aggregate, containing all of the information corresponding to the event.
* Another would be online blogging. Each user would be represented as a document; each post a
document; and each comment, like, or action would be a document. 
* All documents would contain information pertaining to the type of data, such as username, post content, or timestamp when the
document was created.
* More generally speaking, document stores work well with operational datasets for Web and mobile
applications. They were designed with the internet in mind – think JSON, RESTful API, and unstructured
data.
* Other database models may be better solutions when you require ACID transactions. It's not possible for a
document store to handle a transaction that operates over multiple documents and a relational database
may be a better choice in this instance.

Secondly, document databases may not be the right choice if you find yourself forcing your data into an
aggregate-oriented design. If it naturally falls into a normalized/tabular model, this would be another time
to research relational databases instead.

Document databases are currently the most popular of the NoSQL databases in use today, and here you
see some of the more common document databases.

#### 3. Column-Family Databases
Column-Family databases spawned from an architecture that Google created called ***BigTable***. These
databases are therefore also commonly referred to as BigTable clones or Columnar databases. As you can
tell from the name, these databases focus on columns and groups of columns when storing and accessing
data.

Column Families are several rows, each with a unique key or identifier, that belong to one or more
columns. These columns are grouped together in families because they are often accessed together.

It's also important to point out that rows in a column family are not required to share any of the same
columns. They can share all, a subset, or none of the columns and columns can be added to any number
of rows and not to others.

Column-Family databases are great for when you're dealing with large amounts of sparse data. When
compared to row-oriented databases, Column-Family databases can better compress data and save
storage space. In addition, these databases continue the trend of horizontal scalability. Like Key-Value and
Document stores, these databases can handle being deployed across clusters of nodes. Some example use cases for a Column-Family database include event logging and blogs, similar to document databases, but the data would be stored in a different fashion.

For enterprise logging, every application can write to it's own set of columns and have each row key
formatted in such a way to promote easy lookup based on application and timestamp.

Counters are a unique use case. You may come across applications that need an easy way to count or
increment as events occur. Some Column-Family databases, like Cassandra, have special column types
that allow for simple counters. In addition, columns can have a time-to-live parameter, making them
useful for data with an expiration date, like trial periods or ad timing.

On the other hand, Column-Family databases should be avoided if you require traditional ACID transactions provided by relational databases. Reads and writes are only atomic at the row level. And lastly, early in to development, query patterns may change and require numerous changes to the column-family designs. This can be costly and slow down the production timeline. This screen shows some of the more popular types of Column-Family databases.

#### 4. Graph Databases
Finally, Graph Databases, are the last NoSQL variation to review. This database type stands apart from
the previous three types covered because it doesn't follow a few of the common traits previously seen.
From a high level, Graph Databases store information in entities, or nodes…and relationships, or edges.

Graph databases are phenomenal when your data set resembles a graph-like data structure. Traversing all
of the relationships is quick and efficient, but these databases tend not to scale as well horizontally.
Sharding a Graph Database is not recommended since traversing a graph with nodes split across multiple
servers can become difficult and hurt performance.

Graph Databases are also ACID transaction compliant, very much unlike the other NoSQL databases
previously discussed. This prevents any dangling relationships between nodes that don't exist.

Graph Databases can be very powerful when your data is highly connected and related in some way. 
Social networking sites can benefit by quickly locating friends, friends of friends, likes, and so on. And
routing, spacial, and map applications may use graphs to easily model their data for finding close locations
or building shortest routes for directions.

Lastly, recommendation engines can leverage the close relationships and links between products to easily
provide other options to their customers.

Graph Databases are not a good fit for when you're looking for some of the advantages offered by the
other NoSQL variations. When an application needs to scale horizontally, you're going to quickly reach the
limitations associated with these types of data stores.

Another general negative surfaces when trying to update all or a subset of nodes with a given parameter.
These types of operations can prove to be difficult and non-trivial.
This screen shows some of the more popular types of Graph databases.
