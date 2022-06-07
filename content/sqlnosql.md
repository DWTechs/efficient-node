---
title: SQL or NoSQL
---

When developing a microservice API, in most cases you will need to store data in a database.
The great thing about microservice architecture is that you have one database per microservice, meaning you can pick the best system for each one of them.

# Differences between SQL & NoSQL

- SQL databases are relational, NoSQL databases are non-relational.
- SQL databases use structured query language and have a predefined schema. NoSQL databases have dynamic schemas for unstructured data.
- SQL databases are vertically scalable, while NoSQL databases are horizontally scalable.
- SQL databases are table-based, while NoSQL databases are document, key-value, graph, or wide-column stores.
- SQL databases use multi-row transactions, while NoSQL use unstructured data like documents or JSON.


# Structure

SQL database schema always represent relational tabular data, with rules about consistency and integrity. They contain tables with columns (attributes) and rows (records), and keys have constrained logical relationships.
This structure is the easiest to fathom because it is the one most people learnt and are used to work with.

noSQL strutures generally fit into one of those categories : 

- Column-oriented databases transpose row-oriented RDBMSs, allowing efficient storage of high-dimensional data and individual records with varying attributes.
- Key-Value stores are dictionaries which access diverse objects with a key unique to each.
- Document stores hold semi-structured data: objects which contain all of their own relevant information, and which can be completely different from each other.
- Graph databases add the concept of relationships (direct links between objects) to documents, allowing rapid traversal of greatly connected data sets.

# General rules 

**NoSQL trades consistency for performance and scalability.**

Working with these new structures will entirely change the way of developing your microservice in order to be really efficient.

# When to use

Generally, NoSQL is preferred for:

- Graph or hierarchical data
- Data sets which are both large and mutate significantly,
- Businesses growing extremely fast but lacking data schemata.
- Big data

RDBMs is more appropriate when :

- data is conceptually modeled as tabular
- consistency is critical


# More rules

- **Structure**: Do not consider NoSQL if unstructured data does not work for your microservice (ie: you need consistency, integrity, no redundancy...).
- **Size**: NoSQL is usually better for big data.
- **Respone Time & access frequency**: With the right architecture given the context, each solution can be very efficient. It is difficult to extract a general rule on the performance side. Except for very big datasets where NoSQL starts to really shine. 
- **Scaling**: Horizontal scaling is usually easier with NoSQL.


# Performances

NoSQL databases are specifically designed for unstructured data. A particular data entity is stored together and not partitioned. So performing read or write operations on a single data entity is very fast.

SQL databases are normalized. The data is broken down into various logical tables. So SQL databases are fast for joins, queries, updates, etc.

perfomance will depend on the structure of the data.
So it all boils down to the need to get structured or unstructured data.


# Development Speed

With SQL, before entering data into the database, you need to define your schema with a list of columns, types, foreign keys etc. This is time-consuming during the conception phase.

In addition, each change in the table, like adding a column or changing an existing column, requires time to alter the schema before entering different data. Then you will need to update legacy data to fit the new structure.

On the other hand, with NoSQL databases, you don’t need to define a schema to start storing and retrieving data. if the data changes due to business requirements, you can just go ahead and store the data in the new format without restructuring your schema. This is a major advantage of NoSQL databases.

However, because the data is unstructured and mostly unverified before it enters the database, different structures of the same data can exist. Malformed or incorrect data can be inserted and saved. Meaning reliability and consistency features will have to be architected and developed by the team, which adds more complexity to the system. The controllers will also need extra care to be able to handle different cases of data to correctly feed the views.

# Read / Write

In SQL databases, the inserted data is validated to correspond to the schema of the table. This process takes time as we validate each data item against the corresponding column. Once we go schemaless, we can save this precious time. Thus, NoSQL databases provide a larger count of write operations per second as compared to SQL databases. This is especially useful for logging services that need to store huge amounts of log data.

SQL databases, on the other hand, excel at efficiently reading large volumes of data from the database. In scenarios where you are doing multiple read operations per second, a traditional SQL database is very good.


# Scaling 

SQL databases are vertically scalable. You are able to increase the load on a single server by adding more CPU, RAM, or SSD capacity. While horizontal scaling is possible with some SQL databases, NoSQL databases are a lot easier to scale horizontally. Making them ideal to handle higher traffic by adding more containers. Horizontal scaling has a greater overall capacity than vertical scaling, making NoSQL databases the preferred choice for large data sets. 

Note that each databases handle scaling differently. Some NoSQL databases can be impossible to scale horizontaly.

# Into the cloud

Modern brands emphasize interactivity between end-users, justifying decentralized, cloud-based architectures, and exposing diverse new data needing representation. Enter NoSQL, champion of massive, distributed, and morphing data.

But if this non-relational interest caused traditional RDBMSs to flag at all, they are now resurging. SQL remains more accessible, understandable, and most-importantly **"a good enough" solution in most cases**. So why bother.

NoSQL increasingly represents a set of technologies with generalist applicability and inclusiveness. Traditional SQL solutions are also rebranding as generalized databases and connecting with NoSQL. Clearly both paradigms remain equally valid in the modern transition to the cloud.


# Conclusion 

SQL is old and sometimes constraining, but also time-tested and still considered the universal interface.

NoSQL databases are new and flexible, but lack maturity. They require user specialization and a new way of thinking. 

Both models are useful and growing together.

Ultimately, a technology is only valuable when it serves your business and increases ROI.

As usual, do not over-achitecture your project. An objective analysis with weighted criterias will help to make the good decision.
SQL is still relevant in most situations and save a lot of precious time.
