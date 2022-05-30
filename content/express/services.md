# Services

In an MVC pattern the service is part of the model.

It mainly manages the data of the application for example interacting with our database component or file service etc. 

For example it will handle the call to the database and return the result(s) back to the controller. 


Route file example outline:
```javascript
const express = require('express');
const router = express.Router();
const controller = require('../controllers/<controller-name>');

router.get('/', controller.<controller-name>);

#Controller file example :

async function getBlogs(req, res, next) {
  //call to service
  res.send('hello world');
})

#Service

async function getBlogs(req, res, next) {
  //call to database
  return data
})
```

Example in practice
```javascript

require('userController');

router.get('/users', userController.getUsers);

# Controller

require('userService');

function userController() {

  async function getUsers(req: Request, res: Response) {
    const users = await userService.getUsers();
    res.status(200).json(users);
  }

  return { getUsers };
}

# Service - logic simplified for brevity, there maybe some setup logic / error handling etc

require('database');

function userService() {

  async function getUsers() {
    return await database.getUsers();
  }

  async function updateUser(id, user) {
    if (isValid(id)) {
      return await database.updateUser(id, user);
    } else {
      throw new Error(ERRORS.INVALID_ID);
    }
  }

  return { getUsers, updateUser };
}

```