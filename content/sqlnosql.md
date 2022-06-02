---

---

When developping a microservice API, in most cases you will need to store data in a database.
The great thing about microservice architecture is that you have one database per microservice, meaning you can pick the best system for each microservice.

# Differences between SQL & NoSQL

- SQL databases are relational, NoSQL databases are non-relational.
- SQL databases use structured query language and have a predefined schema. NoSQL databases have dynamic schemas for unstructured data.
- SQL databases are vertically scalable, while NoSQL databases are horizontally scalable.
- SQL databases are table-based, while NoSQL databases are document, key-value, graph, or wide-column stores.
- SQL databases use multi-row transactions, while NoSQL use unstructured data like documents or JSON.


# Structure

SQL database schema always represent relational tabular data, with rules about consistency and integrity. They contain tables with columns (attributes) and rows (records), and keys have constrained logical relationships.
This structure is still the best one for most common situations.

noSQL strutures generally fit into one of those categories : 

- Column-oriented databases transpose row-oriented RDBMSs, allowing efficient storage of high-dimensional data and individual records with varying attributes.
- Key-Value stores are dictionaries which access diverse objects with a key unique to each.
- Document stores hold semi-structured data: objects which contain all of their own relevant information, and which can be completely different from each other.
- Graph databases add the concept of relationships (direct links between objects) to documents, allowing rapid traversal of greatly connected data sets.

# General rules 

**NoSQL trades consistency for performance and scalability.**

For the kind of projects we usually work on SQL should be the default choice. From that we can study NoSQL solutions to assess their benefits and drawbacks compared to SQL.

Here is a list of cases where NoSQL might be overkill : 

- **Structure**: Do not consider NoSQL if unstructured data does not work for your microservice (ie: you need consistency, integrity, no redundancy...). In the type of project we develop, we rarely deal with unstructured data. In order to support reliability and consistency features in NoSQL, developers must implement their own code, which adds more complexity to the system.
- **Size**: Do not consider NoSQL for small datasets of only several thousands lines. Unless a NoSQL solution has already been impemented in the project.
- **Respone Time**: Do not consider NoSQL if you do not have specific high performance constraints. Unless a NoSQL solution has already been impemented in the project.
- **Access frequency**: Do not consider NoSQL if your web service does not need high frequency access to the data. Unless a NoSQL solution has already been impemented in the project.
- **Scaling**: Do not consider NoSQL if your web service does not need horizontal scaling. 
- **Weight**: SQL is usually lighter as NoSQL takes more space.

*Keep in mind these rules are highly opinionated and represent our strategy. They do not mean NoSQL is necessarily bad in those situations.*

# Performances

SQL databases are normalized databases where the data is broken down into various logical tables to avoid data redundancy and duplication. In this scenario, SQL databases are faster than their NoSQL counterparts for joins, queries, updates, etc.

On the other hand, NoSQL databases are specifically designed for unstructured data which can be document-oriented, column-oriented, graph-based, etc. In this case, a particular data entity is stored together and not partitioned. So performing read or write operations on a single data entity is faster for NoSQL databases as compared to SQL databases.

In the end, perfomance of each solution will depend on the structure of the data.
So it all boils down to the need to get structured or unstructured data.



# Unstructured data

Unstructured data doesn’t have a predefined schema or data model.

Think of all the media files, documents and emails that your organization stores outside databases — that is unstructured data. In fact, the vast majority of data created by your business each day is unstructured.

NoSQL comes with a pack of constraints that can be disturbing. Knowing how to deal with it and assessing the associated costs is extremely important.

## Consistency

## Integrity

## Redundancy



## Development Speed

In the world of SQL databases, before entering data into the database, you need to define your schema (your table) with a list of columns, types for those columns, and similar. This is time-consuming.

In addition, each change in the table, like adding a column or changing an existing column, requires time to alter the schema before entering different data. You will then need to update legacy data to fit the new structure.

On the other hand, with NoSQL databases, you don’t need to define a schema to start storing and retrieving data. In addition, if the data changes due to business requirements, you can just go ahead and store the data in the new format without restructuring your schema. This is a major advantage of NoSQL databases.

However, this flexibility comes with a price. Because the data is unstructured and mostly unverified before it enters the database, malformed or incorrect data can be inserted and saved. Or different structures of the same data can exist.

Also In order to support reliability and consistency features, developers will need to implement their own code, which adds more complexity to the system. In an MVC pattern it means that your controllers will need extra work to be able to handle different cases of data to correctly feed the views.

## Write Speed

In SQL databases, there is a process that validates that the inserted data corresponds to the schema of the table. This process takes time as we validate each data item against the corresponding column. Once we go schemaless, we can save this precious time. Thus, NoSQL databases provide a larger count of write operations per second as compared to SQL databases. This is especially useful for logging services that need to store huge amounts of log data.

## Read Speed

SQL databases, on the other hand, excel at efficiently reading large volumes of data from the database. In scenarios where you are doing multiple read operations per second, a traditional SQL database can be the right choice.


# update frequency



# Database Scaling 

SQL databases are vertically scalable. You are able to increase the load on a single server by adding more CPU, RAM, or SSD capacity. While horizontal scaling is possible with some SQL databases, NoSQL databases are a lot easier to scale horizontally. Making them ideal to handle higher traffic by adding more containers. Horizontal scaling has a greater overall capacity than vertical scaling, making NoSQL databases the preferred choice for large data sets. 
Note that each NoSQL databases handle scaling differently. So it is necessary to study each of them to decide which one fits your needs.


# Into the cloud

Modern brands emphasize interactivity between end-users, justifying decentralized, cloud-based architectures, and exposing diverse, new data needing representation. Enter NoSQL, champion of massive, distributed, and morphing data.

But if this non-relational interest caused traditional RDBMSs to flag at all, they are now resurging. SQL remains more accessible, understandable, and most-importantly **"the good enough" solution in many many cases**.

NoSQL increasingly represents a set of technologies with generalist applicability and inclusiveness. Traditional SQL solutions are also rebranding as generalized databases and connecting with NoSQL. Clearly both paradigms remain equally valid in the modern transition to the cloud.

# When to use

Generally, NoSQL is preferred for:

- Graph or hierarchical data
- Data sets which are both large and mutate significantly,
- Businesses growing extremely fast but lacking data schemata.

In terms of use cases, this might translate to social networks, online content management, streaming analytics, or mobile applications (ie : gigantic applications).

RDBMs is more appropriate when the data is:

- Small
- Conceptually modeled as tabular
- In systems where consistency is critical

SQL remains the best solution for small business accounting systems, sales databases, or transactional systems like payment processing in e-commerce. When in doubt, SQL is also more appropriate, as RDBMSs are better supported and fault-tolerant.


# business ROI.

SQL is old and sometimes constraining, but also time-tested and increasingly considered a universal interface for data analysis. NoSQL databases are new and flexible, but lack maturity and require user specialization. Pragmatically both models are useful and even growing together.

Ultimately, a technology is only valuable when it serves your business (ie with increased ROI). Even companies like Google, with resources to innovate ad-hoc NoSQL systems from scratch, have found that SQL provided additional value and restored it within critical systems.

# Conclusion 

As usual, do not over-achitecture your project. An objective analysis with weighted criterias will help to make the good decision.