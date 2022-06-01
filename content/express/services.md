
In an MVC pattern the service is part of the model.
It mainly manages the data of the application. 
They live inside the models/ folder.

For example it will handle the call to the database and return it to the controller.


Route file example :

const express = require('express');
const router = express.Router();
const controller = require('../controllers/<controller-name>');

router.get('/', controller.<controller-name>);
Controller file example :

async function getBlogs(req, res, next) {
  //call to service
  res.send('hello world');
})

Service

async function getBlogs(req, res, next) {
  //call to database
  return data
})
