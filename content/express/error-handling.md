
Express out of the box comes with a built in error handler that will automatically catch all synchronous / asynchronous errors that occur inside route handlers and middleware. 

The exception being errors occurring inside asynchronous functions invoked by our route handlers / middleware they must be passed to the next() function for Express to catch and handle them.

For example:

```javascript
// example 1 - error handled automatically 

app.get('/', (req, res) => {
  throw new Error('Some Error'); 
})

// example 2 using next to catch the error from the asynchronous operation and pass it onto Express

app.get('/', (req, res, next) => {
  fs.readFile('/file-does-not-exist', (err, data) => {
    if (err) {
      next(err) ;// Pass errors to Express.
    } else {
      res.send(data);
    }
  });
}

```

**Point to note calling next() with anything other than the string 'route' will cause Express to treat this as an error.**

From Express version 5, route handlers and middleware that return a Promise will call "next(value)" automatically when they reject or throw an error. 

For example:

```javascript
app.get('/user/:id', async (req, res, next) => {
  const user = await getUserById(req.params.id);
  res.send(user);
})
```

When getUserById throws an error or rejects the promise next will be called automatically either with the rejected value or the thrown error, if no value is provided the default error object will be used.

## Catching Errors in Asynchronous Code

You must catch errors occurring in asynchronous Code and pass them to next() function. For example:

```javascript
app.get('/', (req, res, next) => {
  setTimeout(() => {
    try {
      throw new Error('BROKEN');
    } catch (err) {
      next(err);
    }
  }, 100);
})
```

Promises should be used when working with functions that return a Promise to avoid the overhead of the try catch block.

Example:


```javascript
app.get('/', (req, res, next) => {
  Promise.resolve().then(() => {
    throw new Error('BROKEN');
  }).catch(next); // Errors will be passed to Express.
})
```

## Default Error Handler

Express comes with a default error handler which will handle any errors that are encountered within the app as described above.

The error handler is middleware and comes at the end of the middleware function stack. 

We can override the default error handler with a custom error handler, where no custom error handler exists the default handler will be used.

The default error handler will write the response back to the client including the stack trace, unless the NODE_ENV is set to "production" in which case the stack trace is omitted.

When the error is written the following information is added to the response:

* res.statuscode is set to err.status or err.statusCode if the value is in the range of 4xx or 5xx otherwise it will be set to 500.

* res.statusMessage is set according to the status code.

* The body will be set to either the stack trace non production or the status code message for production.

* Any headers specified in the err.headers object

Note if you call next() after the response has started to be written to the client, Express will close the connection and fail the request.

## Custom Error Handlers

Custom error handlers are written in the same way as other middleware functions (
[see Middleware]({{< relref path="middlewares" >}}) ) with the exception that we need to include "err" as the first parameter e.g.

```javascript
app.use((err, req, res, next) => {
  // custom error handler
}
```

The custom error handler must come after all the other middleware components i.e. after all of the other app.use().

It is possible to have several error handling middleware functions one after the other for example a function to log the error, others to respond differently depending on the error and the last to return the error to the client.

Example:

```javascript
const bodyParser = require('body-parser')
const methodOverride = require('method-override')

app.use(bodyParser.urlencoded({
  extended: true
}))
app.use(bodyParser.json());
app.use(methodOverride());
app.use(logErrors);
app.use(clientErrorHandler);
app.use(errorHandler);
```

LogErrors may then write the error to stderr 

```javascript
function logErrors (err, req, res, next) {
  console.error(err.stack);
  next(err);
}
```
And then the clientErrorHandler might look like this, note if the error handler does not call next(), it is responsible for writing the response back to the client, otherwise the application will hang.

```javascript
function clientErrorHandler (err, req, res, next) {
  if (req.xhr) {
    res.status(500).send({ error: 'Something failed!' });
  } else {
    next(err);
  }
}
```

Lastly we have our catch all error handler

```javascript
function errorHandler (err, req, res, next) {
  res.status(500);
  res.render('error', { error: err });
}
```

When writing custom error handlers we should in all cases test to see if the response has already started to be sent to the client, in which case we should default to the Express error handler:

```javascript
function errorHandler (err, req, res, next) {
  if (res.headersSent) {
    return next(err);
  }
  res.status(500);
  res.render('error', { error: err });
}  
```

