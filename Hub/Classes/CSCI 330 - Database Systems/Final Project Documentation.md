---
Title: Final Project Documentation
Source: 
Date: 2023-12-08
tags:
---
# To-Do List Project

Name: Christopher Farrer
Date: 12/8/23
Professor: Qiang Hao
Class: CSCI 330 - Database Systems

## Description

This project was designed to give students hands-on experience by building a To-Do List application that interacts with a MySQL or MongoDB database. While the MongoDB backend was provided as a fully functional example, the MySQL database required students to write the CRUD operations that connect with the frontend. 

Figuring out how to correctly interact with the frontend provided real-world exposure to Javascript and many different frameworks such as React, Express.js, Node.js, and Mongoose. Also, configuring the MySQL backend to interact in the same way as the MongoDB backend required in-depth exploration of both types of APIs. 

## Required Dependencies 

Most of these dependencies I installed using homebrew for mac OS on my local machine, with the exception of Postman.

- XAMPP
- Postman
- Node.js
- npm
- nodemon (installed globally)
- component-specific-packages
	- In each of the main folders ("frontend", "backendSQL", and "backendMongoDB"), the package.json file describes folder-specific dependencies such as Mongoose for "backendMongoDB" and mysql for "backendSQL".

## Steps

Configure MongoDB Example:
1) Install dependencies
2) Set up free MongoDB server
3) Link backend to server with ATLAS URI
4) Run frontend and backendMongoDB
5) Test CRUD operations using Postman and ensure database is being updated correctly in MongoDB. 

Configure MySQL Backend:
1) Install dependencies
2) Start MySQL server using XAMPP
3) Generate database and tables
	1) The following code can be used:
```sql
CREATE DATABASE Tasks;
USE Tasks;
CREATE TABLE tasks (
_id VARCHAR(100) NOT NULL,
text VARCHAR(30) NOT NULL,
reminder BOOLEAN NOT NULL,
day VARCHAR(30) NOT NULL,
PRIMARY KEY (_id)
);
```
4) Generate user credentials and input them into the .env folder
	1) This can be done by accessing MySQL directly or by using phpAdmin from XAMPP. I chose the latter as it's more time effective and user friendly
5) Write methods for PUT, POST, GET, and DELETE
6) Run frontend and backendSQL
	1) It's crucial that only one backend process is running at a time, as both are set to listen to the same port (5001).
7) Test each method and CRUD operations using Postman and ensure records are being updated correctly in the MySQL database.

## Methods

The MongoDB backend was provided fully functional. Thus, stating the implementation for each method feels trivial. While researching them did provide insight into the Mongoose ODM, the main purpose of the project was to write the SQL backend. So, below I've listed my implementation of the CRUD operations relevant to the backendSQL folder with a brief explanation on each. 

### SQL Backend CRUD Operations

#### Create (Insert) implementation:

```javascript
/* ADD A NEW TASK */
router.route("/").post((req, res) => {
const newTask = {
_id: uuidv4(),
text: req.body.text,
reminder: req.body.reminder,
day: req.body.day,
};

let sql = "INSERT INTO tasks SET ?";

let query = db.query(sql, newTask, (err) => {
if (err) throw err;
res.json({ result: newTask });
});
});
```
The req information represents the user-input from the frontend when the user clicks the "Save Task" button. The Task field is represented as "text", Day & Time as "day", and Set Reminder as "reminder". Part of the assignment was not to touch the frontend implementation, however, the design could be refactored to store Day & Time more strictly as a DATETIME attribute instead of a string. 

#### Retrieve (get) implementation:
```javascript
/* GET A TASK */
router.route("/:id").get((req, res) => {
let taskId = req.params.id;
let sql = "SELECT * FROM tasks WHERE _id = ?";

let query = db.query(sql, [taskId], (err, result) => {
if (err) throw err;
res.json({ result: result[0] });
});
});
```
Using the id parameter, we can lookup a specific record or task by querying the database. 

#### Update (put) implementation:
```javascript
/* UPDATE A TASK */

router.route("/:id").put((req, res) => {

// Define variables and queries
let taskId = req.params.id;
let sql = "UPDATE tasks SET reminder = NOT reminder WHERE _id = ?";
let taskSQL = "SELECT text, reminder, day FROM tasks WHERE _id = ?";
let text;
let reminder;
let day;

// Update database
let query = db.query(sql, [taskId], (err) => {
if (err) throw err;
});

// Return updated task
let taskQuery = db.query(taskSQL, [taskId], (err, result) => {
if (err) throw err;
text = result[0].text
reminder = result[0].reminder
day = result[0].day
let task = {
"_id": taskId,
"text": text,
"reminder": reminder,
"day": day
}
res.json({ result: task});
})
});
```
For the purposes of this application, we only dynamically update the reminder field. When a user double-clicks a task in the frontend, the put method is called to flip the remind field and return the updated task to the table. When reminder = 1 or true, a green sidebar is shown on the To-do List. When reminder = 0 or false, the green bar disappears. 
Because double clicking a task only provides us with the id parameter and no req.body, I chose to tackle this method using two database queries. The first updates the record using the id, and the second collects all the information for the updated task and returns it in json form as the response. 

#### Delete implementation

```javascript
router.route("/:id").delete((req, res) => {
let taskId = req.params.id;
let sql = "DELETE FROM tasks WHERE _id = ?";

let query = db.query(sql, [taskId], (err) => {
if (err) throw err;
res.json({ result: "Task deleted successfully" });
});
});
```
This method is fairly straight-forward. Using the id parameter, we can pass in the id to a sql query that deletes the task from our database. This is called when a user clicks the red "x" next to a task in the frontend. In our implementation, there's no way for a user to pass in an id for a task that doesn't exist, so we don't have to worry too much about throwing a 404 error. 

#### Security
It's important to note that we're passing in parameters into our query functions rather than treating the id as a string and plugging it into the sql variable. While unlikely, this practice makes the code less vulnerable to SQL injections.


## Testing Documentation

Here I've provided screenshots on my testing of each relevant operation. 
### Post

Before clicking send:
![[Screenshot 2023-12-08 at 2.01.24 PM.png]]

After:
![[Screenshot 2023-12-08 at 2.03.00 PM.png]]
![[Screenshot 2023-12-08 at 2.03.15 PM.png]]
As you can see, the record successfully was added to the database and is shown in the frontend. 
### Get

![[Screenshot 2023-12-08 at 2.05.10 PM.png]]
After copying the id associated with the "Walk the dog" task and pasting it into the path, the get operation successfully returns the correct record.

### Put

Before:
![[Screenshot 2023-12-08 at 2.06.40 PM.png]]

After:
![[Screenshot 2023-12-08 at 2.06.55 PM.png]]
![[Screenshot 2023-12-08 at 2.08.54 PM.png]]
As you can see, the record successfully updates the reminder field, which, after refreshing the web page, is represented by the green sidebar. 

### Delete 

Before:
![[Screenshot 2023-12-08 at 2.07.26 PM.png]]

After:
![[Screenshot 2023-12-08 at 2.07.41 PM.png]]
![[Screenshot 2023-12-08 at 2.01.24 PM.png]]
As you can see, the record associated with the id we passed in is successfully deleted from the database. 

## Guiding Questions

This sections directly addresses the prompts given in the project description

### How is the frontend working with the backend?

The frontend refers to the part of the application that users directly interact with. In this case, it's represented by our frontend file, which provides the HTML, CSS, and Javascript necessary to display and interact with the To-Do list in the browser. In our case, the frontend communicates with the local host (my personal computer) via port 3000. 

The backend refers to any part of the application that the user does not interact with. Our backend is configured to connect to a database server. In this case, that's over the MySQL default port 3306. The actual backend server, however, is on port 5001. This is the port that our frontend is listening to for data, and is specified in the .env folder. Data is first sent from the frontend to our backend via port 5001, then from our backend to the MySQL database via port 3306, then a response is sent back in opposite order. 

### What role the database play in supporting our backend?

Our database how we store and retrieve information for our application. In this case, it's where we store the tasks given from the user.

### What similarities and differences do MongoDB and MySQL have?

#### Similarities
- Both provide high-performance database management, and are scalable to large applications
#### Differences
- MongoDB is a non-relational database, while MySQL is a relational database
	- This means MongoDB is schema-free, so it doesn't have a defined database structure. MySQL on the other hand has a strictly enforced schema or database structure. 
- MongoDB uses JSON-like documents and files that are JS supported, while MySQL stores data in tables with rows and columns. 
- MongoDB is faster than MySQL

#### Use Cases 

MongoDB: 
Easier to scale and implement, predominately used in big data and real-time data integration.

MySQL:
Primarily used for heavily-trafficked websites and logging applications. Can also be used for data science purposes. 
