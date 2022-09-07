---
Title: Object–relational mapping in the Javascript world
---
WIP

RM in computer science is a programming technique for converting data between type systems using object-oriented programming languages.
This creates, a "virtual object database" that can be used from within the programming language.

In object-oriented programming, data-management tasks act on objects. For example, consider an address book entry that represents a single person along with zero or more phone numbers and zero or more addresses. This could be modeled in an object-oriented implementation by a "Person object" with an attribute/field to hold each data item that the entry comprises: the person's name, a list of phone numbers, and a list of addresses. The list of phone numbers would itself contain "PhoneNumber objects" and so on. Each such address-book entry is treated as a single object by the programming language (it can be referenced by a single variable containing a pointer to the object, for instance). Various methods can be associated with the object, such as methods to return the preferred phone number, the home address, and so on.

By contrast, many popular database products such as SQL database management systems (DBMS) are not object-oriented and can only store and manipulate scalar values such as integers and strings organized within tables. The programmer must either convert the object values into groups of simpler values for storage in the database (and convert them back upon retrieval), or only use simple scalar values within the program. Object–relational mapping implements the first approach.

The heart of the problem involves translating the logical representation of the objects into an atomized form that is capable of being stored in the database while preserving the properties of the objects and their relationships so that they can be reloaded as objects when needed. If this storage and retrieval functionality is implemented, the objects are said to be persistent.

If you know Javascript enough you can already see the waste of energy in this transformation...

Indeed While this approach seems completely appropriate for compiled strictly object oriented languages, it appears that Javascipt prorotype approach is natively a lot more friendly with the data coming from the database.



## Overview

Implementation-specific details of storage drivers are generally wrapped in an API in the programming language in use, exposing methods to interact with the storage medium in a way which is simpler and more in line with the paradigms of surrounding code.

The following is a simple example, written in C# code, to execute a query written in SQL using a database engine.

var sql = "SELECT id, first_name, last_name, phone, birth_date, sex, age FROM persons WHERE id = 10";
var result = context.Persons.FromSqlRaw(sql).ToList();
var name = result[0]["first_name"];
In contrast, the following makes use of an ORM-job API which makes it possible to write code that naturally makes use of the features of the language.

var person = repository.GetPerson(10);
var firstName = person.GetFirstName();
The case above makes use of an object representing the storage repository and methods of that object. Other frameworks might provide code as static methods, as in the example below, and yet other methods may not implement an object-oriented system at all. Often the choice of paradigm is made for the best fit of the ORM into the surrounding language's design principles.

var person = Person.Get(10);
Usually, the framework will expose some filtering and querying functionality for accessing and modifying subsets of the storage base. The code below queries for people in the database whose ID value is '10'.

var person = Person.Get(Person.Properties.Id == 10);


## Comparison with traditional data access techniques

Compared to traditional techniques of exchange between an object-oriented language and a relational database, ORM often reduces the amount of code that needs to be written.[2]

Disadvantages of ORM tools generally stem from the high level of abstraction obscuring what is actually happening in the implementation code. Also, heavy reliance on ORM software has been cited as a major factor in producing poorly designed databases.[3]

## Challenges
A variety of difficulties arise when considering how to match an object system to a relational database. These difficulties are referred to as the object–relational impedance mismatch.

An alternative to implementing ORM is use of the native procedural languages provided with every major database. These can be called from the client using SQL statements. The Data Access Object (DAO) design pattern is used to abstract these statements and offer a lightweight object-oriented interface to the rest of the application.

### The object–relational impedance mismatch 

It is a set of conceptual and technical difficulties that are often encountered when a relational database management system (RDBMS) is being served by an application program (or multiple application programs) written in an object-oriented programming language or style, particularly because objects or class definitions must be mapped to database tables defined by a relational schema.

### Data type differences
A major mismatch between existing relational and OO languages is the type system differences. The relational model strictly prohibits by-reference attributes (or pointers), whereas OO languages embrace and expect by-reference behavior. Scalar types and their operator semantics can be vastly different between the models, causing problems in mapping.

For example, most SQL systems support string types with varying collations and constrained maximum lengths (open-ended text types tend to hinder performance), while most OO languages consider collation only as an argument to sort routines and strings are intrinsically sized to available memory. A more subtle, but related example is that SQL systems often ignore trailing white space in a string for the purposes of comparison, whereas OO string libraries do not. It is typically not possible to construct new data types as a matter of constraining the possible values of other primitive types in an OO language.

### Structural and integrity differences
Another mismatch has to do with the differences in the structural and integrity aspects of the contrasted models. In OO languages, objects can be composed of other objects—often to a high degree—or specialize from a more general definition. This may make the mapping to relational schemas less straightforward. This is because relational data tends to be represented in a named set of global, unnested relation variables. Relations themselves, being sets of tuples all conforming to the same header (see tuple relational calculus) do not have an ideal counterpart in OO languages. Constraints in OO languages are generally not declared as such, but are manifested as exception raising protection logic surrounding code that operates on encapsulated internal data. The relational model, on the other hand, calls for declarative constraints on scalar types, attributes, relation variables, and the database as a whole.

### Manipulative differences
The semantic differences are especially apparent in the manipulative aspects of the contrasted models, however. The relational model has an intrinsic, relatively small and well-defined set of primitive operators for usage in the query and manipulation of data, whereas OO languages generally handle query and manipulation through custom-built or lower-level, case- and physical-access-path-specific imperative operations. Some OO languages do have support for declarative query sublanguages, but because OO languages typically deal with lists and perhaps hash tables, the manipulative primitives are necessarily distinct from the set-based operations of the relational model.[citation needed]

### Transactional differences
The concurrency and transaction aspects are significantly different also. In particular, transactions, the smallest unit of work performed by databases, are much larger in relational databases than are any operations performed by classes in OO languages. Transactions in relational databases are dynamically bounded sets of arbitrary data manipulations, whereas the granularity of transactions in an OO language is typically on the level of individual assignments to primitive-typed fields. In general, OO languages have no analogue of isolation or durability, so atomicity and consistency are only ensured when writing to fields of those primitive types.

### Knowing SQL is an excellent skill

This is probably the main issue in my opinion. SQL is a very important skill to master as a web developer. Most developers using orm lose this skill because of the level of abstraction. Leading to massive performance issues. 

### Technical debt issues



## Javascript

As one of the core technologies of the World Wide Web, alongside HTML and CSS. Approximately 98% of websites use JavaScript on the client side for webpage behavior,

JavaScript is a high-level, often just-in-time compiled language that conforms to the ECMAScript standard.[14] It has dynamic typing, prototype-based object-orientation, and first-class functions. It is multi-paradigm, supporting event-driven, functional, and imperative programming styles.

JavaScript engines were originally used only in web browsers, but are now core components of some servers and a variety of applications. The most popular runtime system for this usage is Node.js.

Node.js brings event-driven programming to web servers, enabling development of fast web servers in JavaScript. Developers can create scalable servers without using threading, by using a simplified model of event-driven programming that uses callbacks to signal the completion of a task.[31] Node.js connects the ease of a scripting language (JavaScript) with the power of Unix network programming.

## Green IT and performances

writing SQL queries gives the ability to fine tune your request to a point that an ORM cannot attain.


## Conclusion

Simplicity is king.
The strength of Javascript and the reason why it is used so much is dynamic typing and the protoype based orientation. In other word it does not have the strict object oriented approach. So why would you add a strict object oriented structure to the data coming from your database in such a dynamic world.
It makes no sense. If you need a strict object oriented approach there are plenty of other languages that will do that way better. When we choose Javascript we want to build on its strength. Not trying to make it look like aother language. That is the reason why we do not recommend to use an ORM with Node.js.  

