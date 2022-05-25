---
layout: default
title: REST
permalink: /rest/

---

Representational state transfer.

# Api design

Most modern web applications expose APIs that clients can use to interact with the application. A well-designed web API should aim to support two key principles:

- Platform independence. Any client should be able to call the API, regardless of how the API is implemented internally. This requires using standard protocols, and having a mechanism whereby the client and the web service can agree on the format of the data to exchange.

- Service evolution. The web API should be able to evolve and add functionality independently from client applications. As the API evolves, existing client applications should continue to function without modification. All functionality should be discoverable so that client applications can fully use it.

This guidance describes issues that you should consider when designing a web API.

## Organize the APi around resources

Focus on the business entities that the web API exposes. For example, in an e-commerce system, the primary entities might be customers and orders. Creating an order can be achieved by sending an HTTP POST request that contains the order information. The HTTP response indicates whether the order was placed successfully or not. When possible, resource URIs should be based on nouns (the resource) and not verbs (the operations on the resource). The API should not be designed around an internal representation of the data for example a database schema, but rather business entities that it represents, so a request for customer information might include the customer name, address and contact number this information could be stored in one or more SQL tables but our client does not need to know that. This allow us to modify the schema of our database independently of the client requesting the resource.

```
https://adventure-works.com/orders // Good

https://adventure-works.com/create-order // Avoid
```

By constructing URIs correctly, it is possible to sort and prioritize them and thus improve the understanding of the system.

## Define operations in terms of HTTP methods

The HTTP protocol defines a number of methods that assign semantic meaning to a request. The common HTTP methods used by most RESTful web APIs are:

- GET retrieves a representation of the resource at the specified URI. The body of the response message contains the details of the requested resource.
- POST creates a new resource at the specified URI. The body of the request message provides the details of the new resource. Note that POST can also be used to trigger operations that don't actually create resources.
- PUT either creates or replaces the resource at the specified URI. The body of the request message specifies the resource to be created or updated.
- PATCH performs a partial update of a resource. The request body specifies the set of changes to apply to the resource.
- DELETE removes the resource at the specified URI.

The effect of a specific request should depend on whether the resource is a collection or an individual item. The following table summarizes the common conventions adopted by most RESTful implementations using the e-commerce example. Not all of these requests might be implemented—it depends on the specific scenario.

| Resource            | POST                              | GET                                 | PUT                                           | DELETE                           |
| ------------------- | --------------------------------- | ----------------------------------- | --------------------------------------------- | -------------------------------- |
| /customers          | Create a new customer             | Retrieve all customers              | Bulk update of customers                      | Remove all customers             |
| /customers/1        | Error                             | Retrieve the details for customer 1 | Update the details of customer 1 if it exists | Remove customer 1                |
| /customers/1/orders | Create a new order for customer 1 | Retrieve all orders for customer 1  | Bulk update of orders for customer 1          | Remove all orders for customer 1 |

Another example (books):

| Resource          | POST                            | GET                              | PUT                                       | DELETE                         |
| ----------------- | ------------------------------- | -------------------------------- | ----------------------------------------- | ------------------------------ |
| /books            | Create a new books              | Retrieve all books               | Bulk update of books                      | Remove all books               |
| /books/1          | Error                           | Retrieve the details for book 1  | Update the details of book 1 if it exists | Remove book 1                  |
| /books/1/comments | Create a new comment for book 1 | Retrieve all comments for book 1 | Bulk update of comments for book 1        | Remove all comments for book 1 |

---

More information and example on [this link](https://docs.microsoft.com/en-gb/azure/architecture/best-practices/api-design)

