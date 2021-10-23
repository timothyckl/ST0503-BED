04 RESTful Web Services w/ Express

## Table of Contents

1. ExpressJS Basics
    - Middleware & Control Flow
2. Serving Static Web Pages
3. Request & Response Objects
4. RESTful Web Services
    - RESTful Principles
    - PUT vs POST
5. Express Routes
6. Web Service Testing w/ POSTMAN

## ExpressJS Basics

ExpressJS is a prebuilt NodeJS framework that can help you in creating server-side web applications. 

It supports various middleware modules which you can easily apply and use to perform additional tasks on request and response.

Middleware functions allow modification of request and response objects.

For example, upon Express receving a GET request middleware can convert the response data into a suitable format.

> __Note:__
> - Middleware functions run explicitly in the order they are invoked. 
> - When a route gets matched, middleware for that route will execute otherwise other routes will be checked for matches

Resource: [What is Middleware? A simple explanation.](https://jamischarles.com/posts/what-is-middleware-a-simple-explanation)

## Serving Static Web Pages

Within the first_express_server directory, create a server.js and a directory called "public".

```js    
// server.js
var express = require('express');
var serveStatic = require('serve-static');
var app = express();
var port=3000;
var hostname="localhost";

app.use(serveStatic(__dirname + '/public')); //apply middleware with app.use
app.listen(port, hostname, () => {
    console.log(`Server started and accessible via http://${hostname}:${port}/`);
  });
```

```html    
<!-- index.html -->
<html>
    <body>
        hello world!
    </body>
</html>
```
Run server.js with `node server.js`.

## Request & Response Objects

### Request Object

The request object can retrieve incoming data from the client for processing.

The request object contains:
- url
- method
- cookie data
- query parameters 

To test out some of the data we can retrieve from the client, modify server.js to include the below code just before we apply the static resource middleware.

To test data retrieved from a client we can add middleware to server.js:
```js    
// server.js
app.use((req, res, next) => {//create our custom middleware
    console.log(req.url);
    console.log(req.method)
    console.log(req.path);    
    console.log(req.query.id);
    next();
  });
```

Run server.js with `node server.js`. 

### Response Object

The response object constitutes the data returned back to the client.
The response object can be used to: 
- set status
- set content-type 
- redirect to another webpage

Here are some use cases:

```js    
// server.js
app.use(function(req, res, next) {
    console.log(req.url);
    console.log(req.method)
    console.log(req.path);    
    console.log(req.query.id);
    res.type(".html");
    res.status(200).send('<html><body>ooga booga!!</body></html>');
    res.end();
    //res.redirect("https://www.sp.edu.sg");//comment out if we just want to redirect

    //next();//since we are setting the whole response data, do not pass to the next middleware
  });
```

Rerun server.js with `node server.js` and observe the effects of the code.

## RESTful Web Services

__What Are RESTful Web Services?__

Representational State Transfer (REST) is an architectural style that specifies constraints
such as:

- Uniform Interface - Induce desirable properties
    - Performance
    - Scalability
    - Modifiability
- Resource Accessibility
    - Uniform Resource Identifiers (URI)
    - Uniform Resource Locator (URL)
- Stateless Communication Protocol between Client/Server
    - HTTP 
- Standardized Resource Representation
    - JSON 
    - HTML
    -  XML
    -  plain text
    -  PDF
    -  JPEG


### RESTful Principles

- __Resource identification through URI__
    - A RESTful web service exposes a set of resources that identify the targets of the interaction with its clients. 
    - Resources are identified by URIs, which provide a global addressing space for resource and service discovery.
- __Uniform interface__
    - Resources are manipulated using Create, Read, Update, Delete (CRUD) operations: PUT, GET, POST, and DELETE. 
- __Self-descriptive messages__
    - Resources are decoupled from their representation so that their content can be accessed in a variety of formats.
- __Stateless interactions__
    - Interactions with resources are stateless/self-contained.
    - Stateful interactions are based on the concept of explicit state transfer.
    - Several techniques exchange state
        - URI rewriting
        - cookies
        - hidden form fields
    -  State can be embedded in response messages to point to valid future states of the interaction. 
 
### HTTP Methods

|Method|Operation performed|Quality|
|-|-|-|
|GET|Read a resource|Safe|
|PUT|Insert a new resource __OR__ update if the resource already exists.|Idempotent|
|POST|Insert a new resource. Also can be used to update an existing resource.|N/A|
|DELETE|Delete a resource|Idempotent|

Reference: [HTTP methods: Idempotency and Safety](https://www.mscharhag.com/api-design/http-idempotent-safe)

### PUT vs POST

Key differences between PUT and POST is that PUT is idempotent while POST is not. 
PUT requests do not change a servers state.
PUT requests must always specify the complete URI of the resource
POST requests create new resources and updates if it already exists.

## Express Routes

Express allows for simply coded middleware with `app.VERB(route, callback)` adding to the middleware chain.
Middleware is only executed when HTTP verb and routes from the client request __match__.
The `app.all()` function can be used to route all types of HTTP request.

Reference: [Express.js | app.all() Function](https://www.geeksforgeeks.org/express-js-app-all-function/)

Create the route for api/user and a new file server.js:

```js
// server.js
var express = require('express');
var bodyParser = require('body-parser');
var port = 8081; //use another port 8081 for this exercise
var hostname = "localhost";

var app = express();

var urlencodedParser = bodyParser.urlencoded({ extended: false });
app.use(urlencodedParser);//attach body-parser middleware
app.use(bodyParser.json());//parse json data

//VERB + URL 
app.get('/api/user', function (req, res) {

   res.status(200);
   res.type(".html");
   res.end("Data of all users sent!");

});

app.listen(port, hostname, () => {
    console.log(`Server started and accessible via http://${hostname}:${port}/`);
  });
```

Run the server with `node server.js`

## Web Service Testing w/ POSTMAN
#
