---
layout: default
title: REST
permalink: /rest/

---

# Api design

A well-designed web API should aim to support two key principles:

- Platform independence. Any client should be able to call the API, regardless of how the API is implemented internally. This requires using standard protocols, and having a mechanism whereby the client and the web service can agree on the format of the data to exchange.

- Service evolution. The web API should be able to evolve and add functionality independently from client applications. As the API evolves, existing client applications should continue to function without modification. All functionality should be documented so that client applications can fully use it.

## Organize the APi around resources

Focus on the business entities that the web API exposes. For example, in an e-commerce system, the primary entities might be customers and orders. Creating an order can be achieved by sending an HTTP POST request that contains the order information. The HTTP response indicates whether the order was placed successfully or not. 

When possible, resource URIs should be based on nouns (the resource) and not verbs (the operations on the resource).

```
https://adventure-works.com/orders // Good

https://adventure-works.com/create-order // Avoid
```

By constructing URIs correctly, it is possible to sort and prioritize them and thus improve the understanding of the system.

The API should not be designed around an internal representation of the data. For example a database schema, but rather business entities that it represents, so a request for customer information might include the customer name, address and contact number. this information could be stored in one or more SQL tables but our client does not need to know that.
This allows us to modify the schema of our database independently of the client requesting the resource.
