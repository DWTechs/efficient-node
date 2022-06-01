
In an MVC pattern the service is part of the model.
It mainly manages the data of the application. 
Services live inside the models/ folder.

For example it will handle the call to the database and return it to the controller.

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

Router File

```javascript

const userController = require('userController');

router.get('/users', userController.getUsers);

```

Controller File

```javascript
const userService = require('userService');

  async function getUsers(req: Request, res: Response) {
    const users = await userService.getUsers();
    res.status(200).json(users);
  }

  export = { getUsers };
```

Service File - logic simplified for brevity, there maybe some setup logic / error handling etc
```javascript

const database = require('database');

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

export = { getUsers, updateUser };
```