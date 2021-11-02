03 HTTP Server w/ Node

## Table of Contents

1. HTTP
    - Request Methods & Structure
    - Response Structure & Code
2. JSON
3. Creating a Node Server
    - HTTP, Path & File Modules
    - HTTP Server Setup

## HTTP

Hypertext Transfer Protocol is an application layer protocol used for communicating between client and server.

HTTP actions such as GET, POST, PUT, DELETE, TRACE,OPTIONS, CONNECT are used to communicate with the server

A request message contains the HTTP verb and target URL with an empty request body.

When the server receives the request, it will retrieve the request data and package it in an appropriate format and send the data back to the client. Data is typically sent in html/css/js or JSON format.

![](https://i.imgur.com/RK5ISHq.png)

### HTTP Request Structure

![](https://i.imgur.com/0TxytzW.png)

### HTTP Response Structure

![](https://i.imgur.com/fXX9ysQ.png)

### Response Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 301 | Moved Permanently |
| 304 | Not Modified |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 422 | Unprocessable Entry|
| 500 | Internal Server Error|
| 505 | HTTP Version Not Supported|

A server's response is organized into three parts:

- Status line
    - Contains response codes 
- Response header
   - Contains metadata for the HTTP Response message as key-value pairs
- Response body
    - Contains the requested information in the format specified

## JSON

JSON stands for JavaScript Object Notation, it is a lightweight format used for storing and transporting data.

### Features of JSON

- Light-weight
- Language independent/Scalable
- Text based and human readable

### Working with JSON 

```js    
const student1={
   "name":"John",
   "age":"18",
   "course":"DIT"
};

// Accessing values with property name 
console.log(student1.name);
console.log(student1.age);
console.log(student1.course);

// Converting JS object to string
const studentStr = JSON.stringify(student1);
```

## Creating a Node Server

To build our own web server, a few built-in Node JS modules are needed:

1. http
    - provides a high-performing foundation for an HTTP stack
2. path
    - provides resolving of full paths, check of file paths etc 
3. fs
    - provides file reading, checking purposes

### HTTP Module

Supports the `createServer()` function which takes a callback with request and response objects

1. The request object represents the HTTP request and contains properties for the request query string, parameters, body, HTTP headers, etc.

2. The response object specifies the HTTP response when app gets an HTTP request. The response is sent back to the client browser and allows you to set new cookies value that will write to the client browser.


### Path Module

The path module allows tocheck if a file exists or examine more details about a file, such as the file extension. 

It also has function which will allow us to convert a relative path into an absolute for a file. 

## HTTP Server Setup

Create a directory called "public" in your working directory. 
It should follow a similar hierarchy:
- nodeJS
    - first_node_server
        - public 

Initialize a package.json file in the first_node_server folder with ```npm init```  
and create the following JS files:

```js    
// server.js
const http = require('http');
const fs = require('fs');
const path = require('path');

const hostname = 'localhost';
const port = 3000;
const server = http.createServer((req, res) => {
    console.log('Request for page ' + req.url + ' using ' + req.method + ‘method’);
    if (req.method == 'GET') {
      var fileUrl=req.url;

      if (req.url == '/') //default file is index.html
        fileUrl = '/index.html';
  
      var filePath = path.resolve('./public'+fileUrl);

        fs.exists(filePath, (exists) => {
            if (!exists) {
                fileUrl='/error.html';
                filePath = path.resolve('./public'+fileUrl);
            
            }else{
                res.statusCode = 200;
                res.setHeader('Content-Type', 'text/html');
            }
            fs.createReadStream(filePath).pipe(res);
        });
    }
    else {
        fileUrl='/error.html';
        filePath = path.resolve('./public'+fileUrl);
        fs.createReadStream(filePath).pipe(res);

    }
});


server.listen(port, hostname, () => {
  console.log(`Server started and accessible via http://${hostname}:${port}/`);
});
```

```js    
// index.html
<html>
    <body>
        Welcome to Node JS!!
    </body>
</html>

// error.html
<html>
    <body>
        File does not exist or web server does not support post method!
    </body>
</html>
```

To run our server, type the following into the terminal:

```bash
node server.js
# or
nodemon server. js # require installation of nodemon module
```
