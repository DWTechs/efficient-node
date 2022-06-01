---
title: MVC for REST APIs
---

# What is the MVC pattern

MVC is a paradigm concerned with how object oriented systems could have UIs.
It helps break up the code into separate components. This way, it is much easier to manage and make changes to either side without them interfering with each other.

It is a simple concept. The code is divided into three components :

- Model for data processing and business logic
- View for the graphical user interface representing the model state
- Controller for the link between View and models. The brains that controls how data is displayed

The controller takes in inputs from the route and turns them into commands which the model can interpret. then it receives the end result from the model and turns it into a response the view can display.

In a web application you can summarize the commmunication between front-end and back-end as *a client sending REST request to a server, the routing matching the requested URL to the controller action, which calls the model(s) for data gathering &processing and return the result back to the client as a HTML page (view) or Json data (API)*.

Early web frameworks took the general idea of separating out business, data and view logic and applied the principle to how they structured the web application. For example Symfony follows MVC guidelines and Angular MVVM is derived from MVC as well. 

# MVC applied to REST APIs

For a modern web application using REST and a static website as front-end, the REST API does not generate a GUI anymore. Most of the time it returns data in JSON format.

The generated JSON can be thought of as the 'view' but other than this the 'View' part of the MVC pattern is not relevant here. Most importantly it is not telling us how to properly separate our code.

# MRC pattern

We will replace 'views' by 'routes' in order to have a clear list of routes with no business logic in it.

So we replace 'MVC pattern' by 'MRC pattern' and separate our code into 3 folders :

- Models/ for handling all of the data and business logic.
- Routes/ for a clear list of routes available
- Controllers/ for the link between routes and models.

The models folder may have separate sub folders (services, entities) depending on the database and the ORM you will use.
In any case you need to understand that we are talking about models in an MVC point of view here.
Meaning that it is not just the data model. It includes all the business logic (services, data models/entities...)

In a micro service architecture 'routes' and 'controllers' folders should not be too crowded, So no subfolders should be needed.
If you feel that you need one then maybe it is time think of creating another micro service.


You will learn more on how to separate your code in the [express chapter](/express/).