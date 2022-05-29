
Swagger is a set of tools created to facilitate the design and documentation of REST APIs according to the 
[Open API Specifications.](https://www.openapis.org/about) 

The API can be written first in Swagger using a design first approach or can be used to document an existing API.

Once the API has been documented this documentation can be made available to other developers on a "documentation" route as part of an API. Via the documentation API it is also possible to call the various routes of the documented API to better understand the responses and usage of this API.

Swagger documentation can be written using JSON or YAML.

In the example below we look at installing Swagger inside a Node.js / TypeScript project.

## Installation

This install makes use of Swagger-ui-express *and swagger-jsdoc*, and assumes you already have a basic node project set-up with Express.
 
 ```
npm i swagger-ui-express swagger-jsdoc
// npm i --save-dev @types/swagger-jsdoc @types/swagger-ui-express
 ```

Having installed the above packages the next step is to configure Swagger inside of our application:

1) In the root of the node project create a folder called "swagger" and create a file "swagger.config.ts"
2) Inside the file create the following:
 ```
 export const swaggerOptions = {
    definition: {
      openapi: "3.0.0",
      info: {
        title: "Sogeti Express Template API with Swagger",
        version: "0.1.0",
        description:
          "This is a simple CRUD API application made with Express and documented with Swagger",
        license: {
          name: "MIT",
          url: "https://spdx.org/licenses/MIT.html",
        },
        contact: {
          name: "Sogeti",
        },
      },
      servers: [
        {
          url: "http://localhost:8080/",
        },
      ],
    },
    apis: ["./swagger/*.yaml"],
  };
 ```

 * openapi - defines the version of the OpenAPI specification we are using to document our API.
 * info - Contains general meta data descirbing this API for more information on the content of the info block see [here](https://spec.openapis.org/oas/v3.1.0#info-object). This information is what will be displayed at the top of our API documentation so should be informative and describe our API.
 * servers - This defines the servers that are hosting our application, we can list multiple servers here to cover different environments e.g. Prod, UAT, dev etc. More information on the server object can be found [here](https://spec.openapis.org/oas/v3.1.0#server-object)
 * apis - this defines the path to where our API documentation resides in this instance in a root folder called swagger within yaml files.

3) In this example our node server is configured in the index.ts file located in the root of the src folder, yours might be called "app" or "server". There is some configuration to do here:
   * First off we need to add the following imports:
  ```
    import swaggerUI from 'swagger-ui-express';
    import swaggerJSDoc from 'swagger-jsdoc';
    import { swaggerOptions } from '../swagger/swagger.config';
  ```
  * Second add the following lines:
  ```
    const API_DOCS_ROUTE = '/api-docs';
    const specs = swaggerJSDoc(swaggerOptions);	
  ```
  * next add, these should be added after you have defined your app as in "const app = express();"

  ```
    app.use(
      API_DOCS_ROUTE,
      swaggerUI.serve,
      swaggerUI.setup(specs)
    );
  ```

  At this point you should be able to start your app and navigate to the api-docs url. Assumming your server is running on localhost and using port 8080 this would be "http://localhost:8080/api-docs/"

  All being well you should see a basic swagger screen:

  ![swagger launch screen](../img/swagger%20launch%20screen.jpg)

If the above screen is not displayed then check the above steps carefully.

## Swagger Basics

Note: This documentation relates to the OpenAPI Spec 3.0 other versions will have a different format.

A Swagger document is broken upto into two sections these being:

* components - used for shared reusable content that is referenced from else where in the document
* paths - used to document our actual API routes

### Components

Components is were we define our reusable elements of our API such as schemas, responses, parameters etc.

### Paths

Paths is were we document the routes of our API. Here we describe everything about our route including parameters and all the possible responses that might be returned in a response. Within the paths when defining the properties we can use the "$ref" to reference an element contained within the components section.

