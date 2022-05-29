---
layout: default
title: Operations
permalink: /rest/

---

# Define operations in terms of HTTP methods

The HTTP protocol defines a number of methods that assign semantic meaning to a request. The common HTTP methods used by most RESTful web APIs are:

- **GET** retrieves a representation of the resource at the specified URI. The body of the response message contains the details of the requested resource.
- **POST** creates a new resource at the specified URI. The body of the request message provides the details of the new resource. Note that POST can also be used to trigger operations that don't actually create resources.
- **PUT** either creates or replaces the resource at the specified URI. The body of the request message specifies the resource to be created or updated.
- **PATCH** performs a partial update of a resource. The request body specifies the set of changes to apply to the resource.
- **DELETE** removes the resource at the specified URI.

The effect of a specific request should depend on whether the resource is a collection or an individual item. The following table summarizes the common conventions adopted by most RESTful implementations using the e-commerce example.

| Resource            | POST                              | GET                                 | PUT                                           | DELETE                           |
| ------------------- | --------------------------------- | ----------------------------------- | --------------------------------------------- | -------------------------------- |
| /customers          | Create a new customer             | Retrieve all customers              | Bulk update of customers                      | Remove all customers             |
| /customers/1        | Error                             | Retrieve the details for customer 1 | Update the details of customer 1 if it exists | Remove customer 1                |
| /customers/1/orders | Create a new order for customer 1 | Retrieve all orders for customer 1  | Bulk update of orders for customer 1          | Remove all orders for customer 1 |
| /orders/2           | Error                             | Retrieve the details for order 2    | Update the details of order 2          | Remove order 2 |


Another example (books):

| Resource          | POST                            | GET                              | PUT                                       | DELETE                         |
| ----------------- | ------------------------------- | -------------------------------- | ----------------------------------------- | ------------------------------ |
| /books            | Create a new books              | Retrieve all books               | Bulk update of books                      | Remove all books               |
| /books/1          | Error                           | Retrieve the details for book 1  | Update the details of book 1 if it exists | Remove book 1                  |
| /books/1/comments | Create a new comment for book 1 | Retrieve all comments for book 1 | Bulk update of comments for book 1        | Remove all comments for book 1 |

---

More information and example on [this link](https://docs.microsoft.com/en-gb/azure/architecture/best-practices/api-design)

