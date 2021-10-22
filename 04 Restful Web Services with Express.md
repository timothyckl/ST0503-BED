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

- a
- b 
- c
- d


### RESTful Principles

- __Resource identification through URI__
    - amongus
- __Uniform interface__
    - amongus
- __Self-descriptive messages__
    - amongus
- __Stateless interactions__
    - amongus

### PUT vs POST

