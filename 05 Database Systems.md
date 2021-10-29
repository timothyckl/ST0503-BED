05 Database Systems

## Table of Contents

1. [Databases](#databases)
    - DBMS
    - Basic Concepts
2. [Relational Model](#relational-model)
    - Relation
    - Attribute
    - Creating a Relational DB
    - Self-Check Quiz
3. [Types of Keys](#types-of-keys-in-relational-model)
    - Candidate Key
    - Self-Check Quiz
    - Primary Key
    - Foreign Key
4. [MySQL Data Types](#mysql-data-types)
5. SQL
6. Database Operations

## Databases

Database refers to an organized collection of structured data to ensure it is easily accessible, managed and update.

An analogy would be the library. The library contains a huge collection of books, ranging of different genres. Here the library represents the database and the books are the data.

### Database Management System (DMBS)

DBMS refers to the computer software/ programs used to Manage (create, update or delete), Protect, and Control the access of the data in a database.

Commonly known relational DBMSs are Oracle, MS SQL and DB2.

### Basic Concepts

TBD

## Relational Model

Let's use Facebook registration as a guide to explore how information are stored within a database.

![](https://i.imgur.com/p0os9Nb.png)

Say you are new to Facebook and you are signing up for an account. After filling up the necessary information, your information will be captured and reflected in the following format:

|First_Name|Surname|Email_Address|Password|DOB|Gender|
|-|-|-|-|-|-|
|Anna|Lee|Anna_lee@hmail.com|deez420|27/11/1998|Female|

### Relation

The information captured above would be stored in a table format, otherwise known as a relation which represents a two-dimensional table. **Each relation has a name that is representative of the data it captures.** In our case, the above relation could be known as the "User" relation.

### Attribute

Attribute refers to the column name in a table. It **defines the characteristic of the object** and in our case, the "User" relation have 6 attributes that helps define an user which are:

- "First Name"
- "Surname"
- "Email"
- "Password"
- "DOB" (Date of Birth)
- "Gender"

Now, we shall populate a few more rows of user information to simulate an actual table.

|First_Name|Surname|Email_Address|Password|DOB|Gender|
|-|-|-|-|-|-|
|Anna|Lee|Anna_lee@hmail.com|deez420|27/11/1998|Female|
|Brandon|Ong|Brandomong@gmail.com|99kthkx|14/06/1996|Male|
|Celine|Tan|Celine_tan92@imail.com|Qwerty69|22/09/1992|Female|
|Dion|Ng|Diondiondion@jmail.com|PiakPiak1|02/02/1996|Male|
    
### Creating a Relational Database

Key points:

1. Name of relation **MUST** be unique
    - There will be multiple relations created in a database so
        you **cannot** create another relation in the same database
        by the same name.
2. Cells **MUST** be single-valued
    - Cells **cannot** have multiple values, 
        in other words 1 cell can only fit 1 value.
3. Attribute names **MUST** be unique
    - You **cannot** have 2 attribute names by the same name.
3. Each tuple/row in a relation is unique
    - You **cannot** have 2 or more rows of the exact same values.

### Self-Check Quiz

|First_Name|First_Name|Email_Address|Password|DOB|Gender|
|-|-|-|-|-|-|
|Anna|Lee|Anna_lee@hmail.com|deez420|27/11/1998|Female|
|Brandon|Ong|Brandomong@gmail.com|99kthkx|14/06/1996|Male|
|Celine|Tan|Celine_tan92@imail.com|Qwerty69|22/09/1992|Female|
|Dion|Ng|Diondiondion@jmail.com|PiakPiak1|**NULL**|Male|

> **Note:** NULL is a special value allowed in a relational database and the value is UNKNOWN or NOT APPLICABLE. 
> 
> In this case, "DOB" is an optional field and Dion does not want to provide his Date of Birth, hence "NULL" is used to replace the cell's value.

<br>

<details>
<summary>
    Based on the above relation, which of the rule(s) have been violated?
    <br><br>
    &nbsp;&nbsp;&nbsp; 1) Name of relation is unique within a database <br>
    &nbsp;&nbsp;&nbsp; 2) Every cells must be single-valued <br>
    &nbsp;&nbsp;&nbsp; 3) Attribute name in a relation must be unique <br>
    &nbsp;&nbsp;&nbsp; 4) Each tuple/row in a relation is unique <br>
</summary>

<br>
Answer:<br>
&nbsp;&nbsp;&nbsp; 3) Attribute name in a relation must be unique <br>
&nbsp;&nbsp;&nbsp; 4) Each tuple/row in a relation is unique <br>
</details>

## Types of Keys in Relational Model

In a database, we often identify "keys" to help **establish and identify relationships between tables** as well as to **uniquely identify any record or row of data** inside a table.

### Candidate Key

Candidate key refers to an **attribute** or a **minimal group** of attributes which can uniquely identify a tuple (record) in a relation. 

|First_Name|Surname|Email_Address|Password|DOB|Gender|
|-|-|-|-|-|-|
|Linda|See|lindaS@gmail.com|abc123|19/10/2000|Female|
|David|Lee|davidL@gmail.com|def456|09/01/2001|Male|
|Nick|Lim|nickL@gmail.com|uvw987|09/01/2001|Male|
|Linda|Lee|lindaL@gmail.com|a1b2c3|01/03/2001|Female|

From the above relation, "__Email_Address__" (an attribute) can uniquely identify a user tuple (record) hence it is a __candidate key__.

"First_Name" is not a candidate key as there could be more than 1 person with the same first name, as seen from above where there are multiple "Linda"s under the "First_Name" attribute.

Grouped attributes can be used to form candidate keys. So "__First_Name__" and "__Surname__" can be grouped together to uniquely identify an user record.

> __Note:__ In reality, some may argue that there could be people with the exact same first name and surname, so we can either group more attributes together or simply use the email address (since there are no duplicate email).

### Self-Check Quiz

<details>
<summary>
    Based on the above relation, which of the following attribute(s) can be a candidate key?
    <br><br>
    &nbsp;&nbsp;&nbsp; 1) Email_Address
    <br>
    &nbsp;&nbsp;&nbsp; 2) DOB
    <br>
    &nbsp;&nbsp;&nbsp; 3) Gender
    <br>
    &nbsp;&nbsp;&nbsp; 4) First_Name + Surname
    <br>
    &nbsp;&nbsp;&nbsp; 5) First_Name
    <br>
    &nbsp;&nbsp;&nbsp; 6) Password
</summary>
<br>
Answer:<br>
    &nbsp;&nbsp;&nbsp;&nbsp;1) Email_Address <br>
    &nbsp;&nbsp;&nbsp;&nbsp;4) First_Name + Surname <br>
    &nbsp;&nbsp;&nbsp;&nbsp;6) Password <br>
</details>

### Primary Key

We don't actually need so many identifiers to form relations. Instead, we can __choose one of the most suitable candidate key be the official identifier__ of a relation and this is known as the **Primary key**.

Essentially, candidate keys refer to an attribute or group of attributes in a relation that uniquely identify every row. 

There can be __more than one candidate key__ in a relation, out of which __one__ is chosen as the primary key. 

> __Note:__ No primary key value can be NULL.

### Foreign Key

Foreign key refers to an **attribute** or a group of attributes with a relation that **matches** the **value** of the **primary key** or the **candidate key** of the **home** or **other relation**.

In short, it is an attribute(s) that __creates a relationship between two__. 

User Relation:

|First_Name|Surname|Email_Address|Password|DOB|Gender|
|-|-|-|-|-|-|
|Linda|See|lindaS@gmail.com|abc123|19/10/2000|Female|
|David|Lee|davidL@gmail.com|def456|10/04/2001|Male|
|Nick|Lim|nickL@gmail.com|uvw987|01/01/2002|Male|

Based on the User relation, since "Email_Address" can uniquely identify an user record, we will assign it as the primary key.

Email|Role|Date_Joined|
|-|-|-|
|davidL@gmail.com|User|06/09/2022|
|lindaS@gmail.com|User|28/04/2023|
|nickL@gmail.com|Admin|09/12/2023|

In the Role relation, "__Email__" would be the __primary key__. In addition, "__Email__" of the Role relation is the __foreign key__ referencing the primary key in the User relation.

> __Note:__ The **attribute name** for the primary and foreign key **need not be the same**. However, the **respective values must match**.


## MySQL Data Types

TBD