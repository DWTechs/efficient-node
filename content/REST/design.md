---
layout: default
title: Design
permalink: /rest/

---

# Overview

A well-designed web API should aim to support two key principles:

- Platform independence. Any client should be able to call the API, regardless of how the API is implemented internally. This requires using standard protocols, and having a mechanism whereby the client and the web service can agree on the format of the data to exchange.

- Service evolution. The web API should be able to evolve and add functionality independently from client applications. As the API evolves, existing client applications should continue to function without modification. All functionality should be documented so that client applications can fully use it.

# Organize around resources

REST APIs are designed around resources, which are any kind of object, data, or service that can be accessed by the client.

A resource has an identifier, which is a URI that uniquely identifies that resource. For example, the URI for a particular customer order might be: https://domain-name.com/orders/1.

Focus on the business entities that the web API exposes. For example, in an e-commerce system, the primary entities might be customers and orders. Creating an order can be achieved by sending an HTTP POST request that contains the order information. The HTTP response indicates whether the order was placed successfully or not. 

When possible, resource URIs should be based on nouns (the resource) and not verbs (the operations on the resource).

```
https://domain-name.com/orders // Good

https://domain-name.com/create-order // Avoid
```

By constructing URIs correctly, it is possible to sort and prioritize them and thus improve the understanding of the system.

The API should not be designed around an internal representation of the data. For example a database schema, but rather business entities that it represents, so a request for customer information might include the customer name, address and contact number. this information could be stored in one or more SQL tables but our client does not need to know that.
This allows us to modify the schema of our database independently of the client requesting the resource.

# Main design principles of RESTful APIs using HTTP

- Clients interact with a service by exchanging representations of resources. Many web APIs use JSON as the exchange format. For example, a GET request to the URI listed above might return this response body:

```JSON
{
    "orderId":1,
    "orderValue":99.90,
    "productId":1,
    "quantity":1
}
```

- REST APIs use a uniform interface, which helps to decouple the client and service implementations. For REST APIs built on HTTP, the uniform interface includes using standard HTTP verbs to perform operations on resources. The most common operations are GET, POST, PUT, PATCH, and DELETE.

- REST APIs use a stateless request model. HTTP requests should be independent and may occur in any order. The only place where information is stored is in the resources themselves.
This constraint enables web services to be highly scalable, because any server can handle any request from any client.

- REST APIs are driven by hypermedia links that are contained in the representation. For example, the following shows a JSON representation of an order. It contains links to get or update the customer associated with the order.

```JSON
{
    "orderID":3,
    "productID":2,
    "quantity":4,
    "orderValue":16.60,
    "links": [
        {"rel":"product","href":"https://domain-name/customers/3", "action":"GET" },
        {"rel":"product","href":"https://domain-name/customers/3", "action":"PUT" }
    ]
}
```

- When a client request is made via a RESTful API, it transfers a representation of the state of the resource to the requester or endpoint.
This information, or representation, is delivered in one of several formats via HTTP: JSON, HTML, plain text... JSON is the most popular file format to use because, despite its name, it is language-agnostic, as well as readable by both humans and machines. 

- Headers and parameters contain important identifier information as to the request's metadata, authorization, uniform resource identifier (URI), caching, cookies, and more. 
There are request headers and response headers, each with their own HTTP connection information and status codes.

REST is considered easier to use than a prescribed protocol like SOAP (Simple Object Access Protocol), which has specific requirements like XML messaging, and built-in security and transaction compliance that make it slower and heavier. 
