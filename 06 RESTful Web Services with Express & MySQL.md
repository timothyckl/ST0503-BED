06 RESTful Web Services w/ Express & MySQL

## Table of Contents

1. [RESTful Web Services with Express and MySQL](#restful-web-services-with-express-and-mysql)
    - Setting Up Persistent Storage
2. [RESTful APIs](#restful-apis)
    - Model View Controller
3. [Creating DB Connection w/ mysql Package](#creating-db-connection-with-mysql-package)
    - DB Queries w/ HTTPS Methods

## RESTful Web Services with Express and MySQL

We can integrate web services with data persistent solutions to develop applications with backend systems to store information.


### Setting Up Persistent Storage

Before creating web services to handle CRUD operations on our database, we will have to set it up first. In this case, we will be using MySQL.

> __MySQL Workbench Install (Windows)__: [https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/)

__User Table Fields__ 

|Attribute|Data Type|
|---------|---------|
|  UserID **(Primary Key, Auto Increment)**| int (11) |
| Username| varchar (255) |
| Password| varchar (100) |
|  Email  | varchar (45) |
|  Role   | varchar (45) |

Start MySQL Workbench and login with the dault root account.

Right-click in the "Schemas" tab to the left and select "Create Schema".

![](https://i.imgur.com/daVvTCY.png)

In the "new_schema" page, define the a schema name. Leave other options as default and click "Apply".

![](https://i.imgur.com/v9MwgmL.png)

In the "Apply SQL Script to Database" page, leave everything as default and select "Apply" and "Finish".

Your new schema can be viewed in the "Schemas" tab.

![](https://i.imgur.com/OybYLI9.png)

Right click on "Tables" and select "Create Table...".

![](https://i.imgur.com/xar4WXe.png)

In the "new_table" page, define the table name and columns and select "Apply".

![](https://i.imgur.com/ubaUXjl.png)

In the "Apply SQL Script to Database" page, select "Apply" and "Finish".

Your new table can be viewed in the "Schemas" tab under "furniture_store" and "Tables".

![](https://i.imgur.com/OCCNDF3.png)

To view your tables data, right click the "user" table and select "Select Rows". 

![](https://i.imgur.com/EA1y56T.png)

Enter data into your table and click "Apply".

![](https://i.imgur.com/jvq50XG.png)

In the "Apply SQL Script to Database" page, select "Apply" and "Finish".

Congrats! Now we have necessary data and table in our MySql database.

## RESTful APIs

We will create a RESTful API based on the "user" table structure.

|Route|HTTP Method|POST Body|Result|
|-----|-----------|---------|------|
|/user|GET|N/A|Retrieve all users|
|/user/:id|GET|N/A|Retrieve single user|
|/user|POST|JSON String|Insert new user|
|/user/:id|PUT|JSON String|Update user|
|/user/:id|DELETE|none|Delete single user|

### Model View Controller

MVC is an architectural pattern consisting of three parts: Model, View, Controller.

**Model**: Handles data logic / interaction with database

**View**: It displays the information from the model to the user

**Controller**: It controls the data flow into a model object and updates the view whenever data changes

See: [Everything you need to know about MVC architecture](https://towardsdatascience.com/everything-you-need-to-know-about-mvc-architecture-3c827930b4c1)

## Creating DB Connection with mysql Package

We will be structuring our code using the MVC design pattern. As web services are meant to be consumed by an external view layer, we will only create a controller and model layer for this project.

File Structure:

```
MYFIRSTWS/
┣ controller/
┃ ┗ app.js
┣ model/
┃ ┣ db-config.js
┃ ┗ user.js
┗ server.js
```

### Setting Up Workspace

Initialize package.json

```
npm init -y
```

### Install Packages

```
npm install mysql
npm install body-parser
npm install express
```

### Defining DB Connection (Model Layer)

```js 
// db-config.js
const mysql = require('mysql');

// Connection settings for MySQL database
const dbConnect = {
    getConnection: () => {
        const cnx = mysql.createConnection({
            host: "localhost",
            user: "root",
            password: "root", // enter your own password
            database: "furniture_store"
        });
        return cnx;
    }
};

module.exports = dbConnect;
```

### DB Interactions

We will proceed to design our database calls to access data in the furniture_store schema.

> **Note**: Password should **never** be stored in plain text and retrieved in real life.

```js    
// user.js
const db = require('./db-config');

const userDB = {
    getUser: (userid, callback) => {
        const cnx = db.getConnection();

        cnx.connect(err => {
            if (err) {
                console.log(err);
                return callback(err);
            }
            console.log("Connected to database!");

            const selectUserQuery = "SELECT * FROM ?? WHERE ?? = ?;";
            const values = ["user", "userid", userid];

            cnx.query(selectUserQuery, values, (err, data) => {
                if (err) {
                    console.log(err);
                    return callback(err);
                }
                console.log(data);
                return callback(null, data);
            });
        });
    },
    addUser: (username, email, role, password, callback) => {
        var cnx = db.getConnection();
        
        cnx.connect(err => {
            if (err) {
                console.log(err);
                return callback(err);
            }
            console.log("Connected to database!");

            const insertUserQuery = "INSERT INTO ?? (??, ??, ??, ??) VALUES (?, ?, ?, ?);";
            const values = ["user", "username", "email", "role", "password", username, email, role, password];

            cnx.query(insertUserQuery, values, (err, data) => {
                if (err) {
                    console.log(err);
                    return callback(err);
                }
                console.log(`${data.affectedRows} rows created`);
                return callback(null, data.affectedRows); // Return number of record(s) inserted
            });
        });
    },
    updateUse: (email, password, userid, callback) => {
        var cnx = db.getConnection();
        
        cnx.connect(err => {
            if (err) {
                console.log(err);
                return callback(err);
            }
            console.log("Connected to database!");

            const updateUserQuery = "UPDATE ?? SET ?? = ?, ?? = ? WHERE ?? = ?;";
            const values = ["user", "email", email, "password", password, "userid", userid];

            cnx.query(updateUserQuery, values, (err, data) => {
                if (err) {
                    console.log(err);
                    return callback(err);
                }
                console.log(`${data.affectedRows} rows updated`);
                return callback(null, data.affectedRows);
            });
        });
    },
};

module.exports = userDB;
```

### Defining Routes (Control Layer)

```js    
// app.js
const express = require('express');
const app = express();
const user = require("../model/user");
const bodyParser = require('body-parser');
const urlencodedparser = bodyParser.urlencoded({ extended: false });

app.use(bodyParser()); // parse application/json
app.use(urlencodedparser); // parse application/x-www-form-urlencoded

app.route('/api/user/:userid').get((req, res) => {
    const id = req.params.userid;

    user.getUser(id, (err, data) => {
        if (err) {
            res.status(500).json({ msg: err });
        } else {
            res.json({ data: data });
        }
    });
}).put((req, res) => {
    const password = req.body.password;
    const email = req.body.email;
    const id = req.params.userid;

    user.updateUser(email, password, id, (err, data) => {
        if (err) {
            res.status(err.statusCode).json({ msg: err });
        } else {
            res.status(201).json({ msg: `${data} record updated` });
        }
    });
}).delete((req, res) => {
    const id = req.params.userid;

    user.deleteUser(id, (err, data) => {
        if (err) {
            res.status(500).json({ msg: err });
        } else {
            res.status(200).json({ msg: `${data} record deleted` });
        }
    })
});

app.route('/api/user').post((req, res) => {
    const username = req.body.username;
    const email = req.body.email;
    const role = req.body.role;
    const password = req.body.password;

    user.addUser(username, email, role, password, (err, data) => {
        if (err) {
            res.status(err.statusCode).json({ msg: err });
        } else {
            res.status(201).json({ msg: `${data} record created` });
        }
    });
});

module.exports = app;
```

Reference: [Express Routing](https://expressjs.com/en/guide/routing.html)

### Creating Main Server

```js    
// server.js
const app = require('./controller/app');
const PORT = process.env.PORT || 3000;

app.listen(PORT, () => console.log(`Server listening at http://localhost:${PORT}`));
```

Finally, we can run our server

```
node server.js
```

To test our API, we can either use Postman or a web browser

Using Chrome:

![](https://i.imgur.com/ByFoE8Q.png)

Using Postman:

**GET Method** \
![](https://i.imgur.com/qTphtrt.png)

**Post Method** \
![](https://i.imgur.com/vxo78IM.png)

**PUT Method** \
![](https://i.imgur.com/QWyRxVA.png)

**DELETE Method** \
![](https://i.imgur.com/wrVCHOt.png)

## Furniture App (Extended Exercise)

beep boop ima get this done like in the future...


