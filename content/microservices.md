---
title: What is the Microservices architecture
---

Microservices architecture refers to an architectural style for developing applications where the application is developed as a collection of services that are : 

- Small. faster to develop and Easier to understand.
- Highly maintainable and testable. It is also more resilient as if one piece fails, the whole app does not necessarily go down,
- Loosely coupled, thus highly scalable 
- Independently deployable. Shorter development cycles
- Independently developed. Owned by a small team. More developers can work on the same big application
- Organized around business capabilities. Each service can be developed using the best language and technology for its own purpose.

It allows a large application to be separated into small independent services. Each one having its own realm of responsibility, built to accommodate an application feature and handle discrete tasks.

It also enables the rapid, frequent and reliable delivery of large, complex applications.

Microservices have become more viable thanks to advancements in containerization technologies, thus being very well suited for cloud-based applications.
It also enables an organization to evolve its technology stack more easily.

To serve a single user request, a microservices-based application can call on many internal microservices to compose its response.


Microservices are used to speed up development. 
It is common to compare microservices versus service-oriented architecture. Both have the same objective of breaking up monolithic applications into smaller components, but with different approaches.

Node.js with its very small footprint is very well suited for this type of architecture.


## Challenges

If your client is thinking about shifting to a microservices architecture, he also needs to change the way people work, not just the apps.
Organizational and cultural changes are identified as challenges in part because each team will have its own deployment cadence and will be responsible for a unique service with its own set of customers. Those may not be typical developer concerns, but they will be essential to a successful microservices architecture.

Beyond culture and process, complexity and efficiency are two major challenges of a microservice-based architecture.


## How to Decompose

One of the ways to make a good split between services could be to define services corresponding to business capabilities. A business capability is something a business does in order to provide value to its end users.

Identifying business capabilities and corresponding services requires a high level understanding of the business.

Once the business capabilities have been identified, the required services can be built corresponding to each of these identified business capabilities.

Each service can be owned by a different team who becomes an expert in that particular domain and an expert in the technologies that are best suited for those particular services. This often leads to more stable API boundaries and more stable teams.

## Building and Deploying

After deciding on the service boundaries of these small services, they can be developed by one or more small teams using the technologies which are best suited for each purpose. For example, you may choose to build a User Service in NodeJS with a MySQL database and a Product Recommendation Service with Java and MongoDB.

Once developed, CI/CD pipelines can be setup with any of the available CI servers (Jenkins, TeamCity, etc.) to run the automated test cases and deploy these service independently to different environments (Integration, QA, Staging, Production, etc).

## Design the Individual Services Carefully

When designing the services, carefully define them and think about what will be exposed, what protocols will be used to interact with the service, etc.

It is very important to hide any complexity and implementation details of the service and only expose what is needed by the service’s clients. If unnecessary details are exposed, it becomes very difficult to change the service later as there will be alot of work to determine who is relying on the various parts of the service. Additionally, a great deal of flexibility is lost in being able to deploying the service independently.

## Decentralize Things

There are organizations who have found success with microservices and have followed a model where the teams who build the services take care of everything related to that service. They are the ones who develop, deploy, maintain and support it. There are no separate support or maintenance teams.

Another way to achieve the same is to have an internal open source model. By taking this approach, the developer who needs changes in a service can check out the code, work on a feature, and submit a PR himself instead of waiting for the service owner to pickup and work on needed changes.

For this model to work properly, the proper technical documentation is needed along with setup instructions and guidance for each service so that it’s easy for anyone to pickup and work on the service.

Another hidden advantage of this approach is that it keeps developers focused on writing high quality code as they know that others will be looking at it.

There are also some architectural patterns which can help in decentralizing things. For example, you might have an architecture where the collection of services are communicating via a central message bus. This bus handles the routing of messages from different services. Message brokers like RabbitMQ are a good example.

What tends to happen over time is people start putting more and more logic into this central bus and it starts knowing more and more about your domain. As it becomes more intelligent, that should be avoided as it becomes difficult to make changes which require coordination across separate dedicated teams.

A general advice for those types of architectures would be to keep them relatively “dumb” and let them just handle the routing. Event based architectures seem to work quite well in those scenarios.

## Deploy

It is important to write Consumer Driven Contracts for any API that is being depended upon. This is to ensure that new changes in that API don’t break your API.

In Consumer Driven Contracts, each consumer API captures their expectations of the provider in a separate contract. All of these contracts are shared with the provider so that they gain insight into the obligations they must fulfill for each individual client.

Consumer Driven Contracts must pass completely before being deployed and before any changes are made to the API. It also helps the provider to know what services are depending on it and how other services are depending on it.


## Making Standards

When there are multiple teams taking care of different services independently, it’s best to introduce some standards and best practices — error handling, for example. As might be expected, standards and best practices are not provided, each service would likely handle errors differently, and no doubt a significant amount of unnecessary code would be written several times.

Creating standards is always helpful in long run. It is also important to let others know what an API does and documentation of the API should always be done when creating it. There are tools like Swagger which are very helpful in assisting in development across the entire API lifecycle, from design and documentation, to test and deployment. An ability to create metadata for your API and let users play with it, allows them to know more about it and use it more effectively.

## Service Dependencies

Over time, each service starts depending on more and more services. This can introduce more problems as the services grow, for example, the number of service instances and their locations (host+port) might change dynamically. Also, the protocols and the format in which data is shared might vary from service to service.

Here’s where API Gateways and Service Discovery become very helpful. Implementing an API Gateway becomes a single entry point for all clients, and API Gateways can expose a different API for each client.

The API gateway might also implement security such as verifying that the client is authorized to perform the request. There are some tools which can be used for Service Discovery.

##  Failure

An important point to understand is that microservices are not resilient by default. There will be failures in services. Failures can happen because of failures in dependent services. Additionally, failures can arise for a variety of reasons such as bugs in code, network time outs, etc.

What’s critical with a microservices architecture is to ensure that the whole system is not impacted or goes down when there are errors in an individual part of the system.

There are patterns like Bulkhead and Circuits Breaker which can help achieve better resiliency

## Monitoring and Logging

Microservices are distributed by nature and monitoring and logging of individual services can be a challenge. It is difficult to go through and correlate logs of each service instance and figure out individual errors. Just as with monolithic applications, there is no single place to monitor microservices.

To solve such problems, a preferred approach is to take advantage of a centralized logging service that aggregate logs from each service instance. Users can search through these logs from one centralized spot and configure alerts when certain messages appear.

Standard tools are available and widely used by various enterprises. They collects and aggregate logs which can be searched via a Kibana dashboard indexed by Elasticsearch.
