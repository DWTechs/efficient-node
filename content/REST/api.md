---
layout: default
title: REST
permalink: /rest/

---


# Overview

A REST API (also known as RESTful API) is an Application Programming Interface that conforms to the constraints of REST architectural style and allows for interaction with RESTful web services. REST stands for REpresentational State Transfer and was created by Roy Fielding in 2000 who also co-founded the Apache HTTP Server project and has been heavily involved in the development of HTML.

# What is an API

An API helps you communicate with a system so it can understand and fulfill the request. 

You can think of an API as a mediator between the users or clients and the resources or web services they want to get. It’s also a way for an organization to share resources and information while maintaining security, control, and authentication—determining who gets access to what. 

# What is REST

REST is a set of architectural constraints. 
It is not a protocol nor a standard, so API developers can implement REST in a variety of ways.

When a client request is made via a RESTful API, it transfers a representation of the state of the resource to the requester or endpoint.
This information, or representation, is delivered in one of several formats via HTTP: JSON, HTML, plain text... JSON is the most popular file format to use because, despite its name, it is language-agnostic, as well as readable by both humans and machines. 

Headers and parameters are also important in the HTTP methods of a RESTful API HTTP request, as they contain important identifier information as to the request's metadata, authorization, uniform resource identifier (URI), caching, cookies, and more. 
There are request headers and response headers, each with their own HTTP connection information and status codes.

## Criterias

In order for an API to be considered RESTful, it has to conform to these criteria:

- A client-server architecture made up of clients, servers, and resources, with requests managed through HTTP.
- Stateless client-server communication, meaning no client information is stored between requests, and each request is separate and unconnected.
- Cacheable data that streamlines client-server interactions.
- A uniform interface between components so that information is transferred in a standard form. Meaning that The representation received contains enough information to manipulate it.

REST is considered easier to use than a prescribed protocol like SOAP (Simple Object Access Protocol), which has specific requirements like XML messaging, and built-in security and transaction compliance that make it slower and heavier. 
