
# Controllers

A controller is responsible for controlling the way that a user interacts with an MVC application. It contains the flow control logic and determines what response to send back to a user when a user makes a request.

As seen in the previous chapter, for every route you define a route-handler callback function (ie: a middleware) that will contain the code to compute a proper response.
In MVC pattern ths is exactly what a controller should do.
This is why we put this callback functions into a "controllers" folder.

It helps make things cleaner as your "routes" pages are just a catalog of routes with no code inside. and all the logic is separated in to its own controller.

Click here to learn more about controllers in MVC patterns.

Route file example :

```Javascript
const express = require('express');
const router = express.Router();
const controller = require('../controllers/<controller-name>');

router.get('/', controller.<controller-name>);
```

Controller file example : 

```Javascript
async function getBlogs(req, res, next) {
  res.send('hello world');
})
```
