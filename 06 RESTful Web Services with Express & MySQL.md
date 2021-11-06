06 RESTful Web Services w/ Express & MySQL

## Table of Contents

1. [RESTful Web Services with Express and MySQL](#restful-web-services-with-express-and-mysql)
    - Setting Up Persistent Storage
2. [RESTful APIs](#restful-apis)
    - Model View Controller
3. [Creating DB Connection w/ mysql Package](#creating-db-connection-w/-mysql-package)
    - DB Queries w/ HTTPS Methods

## RESTful Web Services with Express and MySQL

We can integrate web services with data persistent solutions to develop applications with backend systems to store information.


### Setting Up Persistent Storage

Before creating web services to handle CRUD operations on our database, we will have to set it up first. In this case, we will be using MySQL.

> __Install Link for Windows__: [https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/)

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

Your new table can be vied in the "Schemas" tab under "furniture_store" and "Tables".

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
