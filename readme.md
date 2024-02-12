# 	B8IT146: Web and Cloud Application Development

# Lab/Activity 13



**Chapters:** Chapter 13

**Cognitive Levels:** Apply

**Aim:** The student should be able to:

- Create a NodeJs Express Project Application
- Create a database
- Create tables in the database
- Connect Node.js to a database
- Retrieve and add/delete/update records into a database using Node.js
- Render the results on a form
- Use EJS and Express to perform simple CRUD operations on a database from a form

**Tools:** MySQL, SQL, Node.js, Express, Command Line Prompt

**Document Revision Control: 2.0**

# Building a NodeJS project using Express and EJS to perform CRUD operations - Apply

_**In this lab you will create a fully working project with several CRUD operations which uses EJS (Embedded JavaScript).**_ _ **EJS** _ _ **lets us embed JavaScript code in a template language that is then used to generate HTML** _ **.** _ **A solution is available for you to check the codes. We will carry out the following tasks in this project.** _

1. [Download Node Express Module & Application](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step1)
2. [Basic Routing of Node Express Application](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step2)
3. [Make MySQL Database Connection in Node Express Application](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step3)
4. [Fetch & Display Data from MySQL Database](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step4)
5. [Insert Form Data into MySQL Table](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step5)
6. [Edit or Update MySQL Table Data](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step6)
7. [Delete Data From MySQL Table](https://www.webslesson.info/2022/04/insert-update-delete-data-from-mysql-in-node-js-using-express-js.html#step7)

_ **Your project will eventually look like this:** _


![](https://github.com/baz2024/CRUDNodeJsExpressApplication-/blob/main/first.png)
# Step 1- APPLY – Create the Sample\_data table in MySQL needed for our project

You have to run following query, which will create  **sample\_data**  table in your MySQL Database.

##### Create the database

```
create database sample;
use sample;

```
 

#####  Table structure for table `sample_data`** 

```
CREATE TABLE `sample_data` (

`id` int(10) NOT NULL,

`first_name` varchar(250) NOT NULL,

`last_name` varchar(250) NOT NULL,

`age` varchar(30) NOT NULL,

`gender` varchar(30) NOT NULL

) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```
 

##### Dumping data for table `sample_data`
```
 

INSERT INTO `sample_data` (`id`, `first_name`, `last_name`, `age`, `gender`) VALUES

(1, 'John', 'Smith', '26', 'Male'),

(2, 'Donna', 'Hubber', '24', 'Female'),

(3, 'Peter', 'Parker', '28', 'Male'),

(4, 'Tom', 'Muddy', '32', 'Male'),

(6, 'Lisa', 'Ray', '26', 'Female');
```

 
##### Indexes for dumped tables

 

###### Indexes for table `sample_data`

```

ALTER TABLE `sample_data`

ADD PRIMARY KEY (`id`);
```
 
##### AUTO\_INCREMENT for dumped tables

 
 
##### AUTO\_INCREMENT for table `sample_data`
 
```
ALTER TABLE `sample_data`

MODIFY `id` int(10) NOT NULL AUTO\_INCREMENT, AUTO\_INCREMENT=7;
```

# Step 2- APPLY – Create a New CRUD Project which uses EJS(Embedded JavaScript Templates)

Create a new director folder to hold your CRUD project_. Call it CRUD._

_Navigate the location where you want to store your project and run the following commands:_

```
mkdir crud

cd crud
```

# Step 3 - APPLY – Generate the CRUD Project Structure using EJS

Now open the empty CRUD project in VSCode

Under this directory, we have to run following command. This command will install the Express generator.
```
npm install -g express-generator
```
Next install the Express Application, so for this we have to run the following command. This will generate a number of folders in your project such as views, public and routes. Then take a look inside your CRUD project folder.

```
npx express --view=ejs
```
# Step 4 - APPLY – Install the needed dependencies

Next we need to install dependencies, so for this we have to run following command. So this command will install dependencies in Node Express Application. The node module folder will appear after running the next command.

```
npm install
```

![](RackMultipart20240212-1-5or5ms_html_508075602f0ce05.png)

```
npm start
```
Now we want to check the output in the browser. Run the command for the URL:

[http://localhost:3000](http://localhost:3000)

This command will start Node.js server and for checking output in the browser, If you see the following then you have been successful in setting up your project which will use EJS. You can continue.

![](RackMultipart20240212-1-5or5ms_html_267471bf6f4d6c7d.png)

# Step 5 - APPLY – Basic Routing of Node Express Application

Now we want to create a new javascript file in the  **routes**  directory called **sample_data.js**  file. And under this file, we have create simple Node Express application with simple routing for the crud application.

**routes/sample\_data.js**
```
var express =require('express');

var router = express.Router();

router.get("/",function(request, response, next){

response.send('List all Sample Data');

});

router.get("/add",function(request, response, next){

response.send('Add Sample Data');

});

module.exports = router;
```
Next open the **app.js**  file and under this file, add the following code:
```
var sampledataRouter =require('./routes/sample_data');
```
After this, set the route for the sample_data, by adding the following code in  **app.js**  file.
```
app.use('/sample_data', sampledataRouter);
```
Now our simple Node Express Application is ready for checking with simple routing in the browser. Now you can hit following URL in the browser for check output of Node.js Express Application in the browser.

http://localhost:3000/sample_data

http://localhost:3000/sample_data/add

# Step 6 - APPLY – Making a Database Connection in the Node Express Application

If you are making any dynamic application with Database, you need to create Database connection. We are using MySQL Database with Node.js Express Application. So for making the MySQL database connection from Node js Express application, we need to download MySQL node package and with the help of this package, it will do Insert, Update, Delete and Read Database operations in the Node js express application. To install MySQL node package, we need to run following command in command prompt along slide our project.

`npm install mysql2`

After download and install Node JS Express and MySQL package, now we have to go to the text editor and create  **database.js**  file and under this file, we have to write following code in it. So it will make a mysql database connection file in the Node application. The database.js should be at the root directiry crud or at the same level as app.js 

```
//database.js

const mysql =require('mysql2');

var connection = mysql.createConnection({

host :'localhost',

database :'sample',

user :'root',

password :'lab-password'

});

connection.connect(function(error){

if(error)

{

throw error;

}

else

{

console.log('MySQL Database is connected Successfully');

}

});

module.exports = connection;


```
After creating database connection file, next we need to include a reference to that file in javascript server file. Include the database connection file under  **routes/sample\_data.js**  file so that the file will be connected with the mysql database. It will then be able to perform mysql CRUD operations.

**routes/sample\_data.js**
```
var express =require('express');

var router = express.Router();

var database =require('../database');

router.get("/",function(request, response, next){

response.send('List all Sample Data');

});

router.get("/add",function(request, response, next){

response.send('Add Sample Data');

});

module.exports = router;
```
# Exercise 7 - APPLY – Fetch & Display Data from a MySQL Database

In this step, you can learn How to fetch data from MySQL Table and display on the web page in the HTML table format in the Node.js application.

**routes/sample_data.js**
```
var express =require('express');

var router = express.Router();

var database =require('../database');

router.get("/",function(request, response, next){

var query ="SELECT \* FROM sample\_data ORDER BY id DESC";

database.query(query,function(error, data){

if(error)

{

throw error;

}

else

{

response.render('sample_data',{title:'Node.js MySQL CRUD Application', action:'list', sampleData:data});

}

});

});

module.exports = router;
```
To fetch data from database, create a route in the route javascript server file using get() function and under this, write the MySQL query to fetch data from your MySQL table. Under this Route function, execute the MySql Fetch query by using a query() function. This function will execute MySQL fetch query and return the query result, which will be sent to the node.js template file.

Next load the node js template file, by using response.render() function which will load the node js template file. This function has **two** parameters, (1) defining template file name, and in (2) passing the data which can be accessed in the template file. Here you have to define data in json data format.

After this go to the node.js template file, in  **views/sample\_data.ejs**. This file will be loaded in the browser by using the get() function. Here it will use sample file for different operations by using an if condition. Below find the source code for how display the MySql table data in HTML format.

**views/sample_data.ejs**

```
<!doctype html>
<html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

        <title></title>
    </head>
    <body>
        <div class="container">
            <h1 class="text-center mt-3 mb-3"><%= title %></h1>
            <% if(action == 'add') { %>

            <% } else { %>
                
            <div class="card">
                <div class="card-header">
                    <div class="row">
                        <div class="col">Sample Data</div>
                        <div class="col"></div>
                    </div>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <tr>
                                <th>First Name</th>
                                <th>Last Name</th>
                                <th>Age</th>
                                <th>Gender</th>
                                <th>Action</th>
                            </tr>
                            <%
                            if(sampleData.length > 0)
                            {
                                sampleData.forEach(function(data){
                            %>
                            <tr>
                                <td><%= data.first_name %></td>
                                <td><%= data.last_name %></td>
                                <td><%= data.age %></td>
                                <td><%= data.gender %></td>
                                <td></td>
                            </tr>
                            <%
                                });
                            }
                            else
                            {
                            %>
                            <tr>
                                <td colspan="5">No Data Found</td>
                            </tr>
                            <%
                            }
                            %>
                        </table>
                    </div>
                </div>
            </div>

            <% } %>
        </div> 
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
</html>


```
To Fetch and Display output in the browser, you have to hit following url in the browser, which will show you output of Node.js Fetch and Display Data from MySQL Database.

http://localhost:3000/sample_data

## **Step 8 - APPLY – Insert Form Data into a MySQL Database**

In this Node JS CRUD Application, we will Insert Form Data into MySQL table. In this step you can learn how to Insert Data into MySQL Database using Node JS Express Application. To Insert Data into Database, you need to create a HTML Form to get Data from user. So for loading the HTML form in the browser, we need to set a route. See the source code for setting the route to load Add Form in the browser.

**routes/sample_data.js**
```
var express = require('express');

var router = express.Router();

var database = require('../database');

router.get("/", function(request, response, next){

var query = "SELECT * FROM sample_data ORDER BY id DESC";

database.query(query, function(error, data){

if(error)

{

throw error;

}

else

{

response.render('sample_data', {title:'Node.js MySQL CRUD Application', action:'list', sampleData:data});

}

});

});

router.get("/add", function(request, response, next){

response.render("sample_data", {title:'Insert Data into MySQL', action:'add'});

});

module.exports = router;
```

Once you have set the route, you have to create HTML Form in Node Express Template file, as shown below:

**views/sample_data.ejs**

```
<!doctype html>
<html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

        <title></title>
    </head>
    <body>
        <div class="container">
            <h1 class="text-center mt-3 mb-3"><%= title %></h1>
            
            <% if(action == 'add') { %>

            <div class="card">
                <div class="card-header">Sample Form</div>
                <div class="card-body">
                    <form method="POST" action="/sample_data/add_sample_data">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>First Name</label>
                                    <input type="text" name="first_name" id="first_name" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Last Name</label>
                                    <input type="text" name="last_name" id="last_name" class="form-control" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Age</label>
                                    <input type="number" name="age" id="age" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Gender</label>
                                    <select name="gender" class="form-control">
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="mb-3">
                            <input type="submit" name="submit_button" class="btn btn-primary" value="Add" />
                        </div>
                    </form>
                </div>
            </div>

            <% } else { %>
                
            <div class="card">
                <div class="card-header">
                    <div class="row">
                        <div class="col">Sample Data</div>
                        <div class="col">
                            <a href="/sample_data/add" class="btn btn-success btn-sm float-end">Add</a>
                        </div>
                    </div>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <tr>
                                <th>First Name</th>
                                <th>Last Name</th>
                                <th>Age</th>
                                <th>Gender</th>
                                <th>Action</th>
                            </tr>
                            <%
                            if(sampleData.length > 0)
                            {
                                sampleData.forEach(function(data){
                            %>
                            <tr>
                                <td><%= data.first_name %></td>
                                <td><%= data.last_name %></td>
                                <td><%= data.age %></td>
                                <td><%= data.gender %></td>
                                <td></td>
                            </tr>
                            <%
                                });
                            }
                            else
                            {
                            %>
                            <tr>
                                <td colspan="5">No Data Found</td>
                            </tr>
                            <%
                            }
                            %>
                        </table>
                    </div>
                </div>
            </div>

            <% } %>

        </div> 

        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
</html>


```
After this form has been submitted, it will send a request to the **add\sample_data**  route, so we need to create route to handle the form data request.

Create the route in  **routes/sample\_data.js**  and under this save the form data into a local variable.

Create the MySQL Insert query and under that will query define the variable in which we have store form data. Run the MySQL insert query and it will insert the form data into your MySQL table in the Node JS application. It will request the web page to the root url in which you can see sample\_data table data with last inserted data.

**routes/sample_data.js**
```
var express = require('express');

var router = express.Router();

var database = require('../database');

router.get("/", function(request, response, next){

var query = "SELECT * FROM sample_data ORDER BY id DESC";

database.query(query, function(error, data){

if(error)

{

throw error;

}

else

{

response.render('sample_data', {title:'Node.js MySQL CRUD Application', action:'list', sampleData:data});

}

});

});

router.get("/add", function(request, response, next){

response.render("sample_data", {title:'Insert Data into MySQL', action:'add'});

});

router.post("/add_sample_data", function(request, response, next){

var first_name = request.body.first_name;

var last_name = request.body.last_name;

var age = request.body.age;

var gender = request.body.gender;

var query = `

INSERT INTO sample_data

(first_name, last_name, age, gender)

VALUES ("${first_name}", "${last_name}", "${age}", "${gender}")
`;

database.query(query, function(error, data){

if(error)

{

throw error;

}

else

{

response.redirect("/sample_data");

}

});

});

module.exports = router;
```
Check the output of Insert Form Data inserted into MySQL by using using Node JS in the browser, first you need to start Node.js server from command prompt by run  **npm start**  command and then after go to browser and hit following url.

http://localhost:3000/sample_data/add

# Step 9 - APPLY – Edit or Update MySQL Table Data

Once we have inserted the form data into the MySQL table using Node.js, next we need to show you how to edit or update the table data using our Node.js Express Application.

Create an Edit button in each of MySQL data records in the HTML table. Go to  **views/sample\_data.ejs**  file and under this write following code to create the edit button.

**views/sample\_data.ejs**
```
<!doctype html>
<html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
        <title></title>
    </head>
    <body>
        <div class="container">
            <h1 class="text-center mt-3 mb-3"><%= title %></h1>         
            <% if(action == 'add') { %>
            <div class="card">
                <div class="card-header">Sample Form</div>
                <div class="card-body">
                    <form method="POST" action="/sample_data/add_sample_data">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>First Name</label>
                                    <input type="text" name="first_name" id="first_name" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Last Name</label>
                                    <input type="text" name="last_name" id="last_name" class="form-control" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Age</label>
                                    <input type="number" name="age" id="age" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Gender</label>
                                    <select name="gender" class="form-control">
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="mb-3">
                            <input type="submit" name="submit_button" class="btn btn-primary" value="Add" />
                        </div>
                    </form>
                </div>
            </div>
            <% } 
	else { %>           
            <div class="card">
                <div class="card-header">
                    <div class="row">
                        <div class="col">Sample Data</div>
                        <div class="col">
                            <a href="/sample_data/add" class="btn btn-success btn-sm float-end">Add</a>
                        </div>
                    </div>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <tr>
                                <th>First Name</th>
                                <th>Last Name</th>
                                <th>Age</th>
                                <th>Gender</th>
                                <th>Action</th>
                            </tr>
                            <%
                            if(sampleData.length > 0)
                            {
                                sampleData.forEach(function(data){
                            %>
                            <tr>
                                <td><%= data.first_name %></td>
                                <td><%= data.last_name %></td>
                                <td><%= data.age %></td>
                                <td><%= data.gender %></td>
                                <td>
                    <a href="/sample_data/edit/<%= data.id %>" class="btn btn-primary btn-sm">Edit</a>
                                </td>
                            </tr>
                            <%
                                });
                            }
                            else
                            {
                            %>
                            <tr>
                                <td colspan="5">No Data Found</td>
                            </tr>
                            <%
                            }
                            %>
                        </table>
                    </div>
                </div>
            </div>
            <% } %>
        </div> 
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
</html>


```

After this, go to  **routes/sample_data.js**  and under this file, create new route for fetch a single row of data, and then load that data into HTML form and load that edit data form in the browser.

**routes/sample_data.js**
```
router.get('/edit/:id',function(request, response, next){

var id = request.params.id;

var query =`SELECT * FROM sample_data WHERE id = "${id}"`;

database.query(query,function(error, data){

response.render('sample_data',{title:'Edit MySQL Table Data', action:'edit', sampleData:data[0]});

});

});
```
In this route, we use the MySQL select query to fetch a single row of data, and execute that query to fetch data from MySQL table, after this we send that data to the Node js template file.

After this, again we have go to  **views/sample\_data.ejs**  template file, and under this file, first we have write if condition for load edit form in browser with data.

**views/sample\_data.ejs**

```
<!doctype html>
<html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

        <title></title>
    </head>
    <body>
        <div class="container">
            <h1 class="text-center mt-3 mb-3"><%= title %></h1>
            
            <% if(action == 'add') { %>

            <div class="card">
                <div class="card-header">Sample Form</div>
                <div class="card-body">
                    <form method="POST" action="/sample_data/add_sample_data">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>First Name</label>
                                    <input type="text" name="first_name" id="first_name" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Last Name</label>
                                    <input type="text" name="last_name" id="last_name" class="form-control" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Age</label>
                                    <input type="number" name="age" id="age" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Gender</label>
                                    <select name="gender" class="form-control">
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="mb-3">
                            <input type="submit" name="submit_button" class="btn btn-primary" value="Add" />
                        </div>
                    </form>
                </div>
            </div>

            <% } else if(action == 'edit') { %>
            <div class="card">
                <div class="card-header">Sample Form</div>
                <div class="card-body">
                    <form method="POST" action="/sample_data/edit/<%= sampleData.id %>">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>First Name</label>
                                    <input type="text" name="first_name" id="first_name" class="form-control" value="<%= sampleData.first_name %>" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Last Name</label>
                                    <input type="text" name="last_name" id="last_name" class="form-control" value="<%= sampleData.last_name %>" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Age</label>
                                    <input type="number" name="age" id="age" class="form-control" value="<%= sampleData.age %>" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Gender</label>
                                    <select name="gender" id="gender" class="form-control">
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="mb-3">
                            <input type="submit" name="submit_button" class="btn btn-primary" value="Edit" />
                        </div>
                    </form>
                    <script>
                    document.getElementById('gender').value="<%= sampleData.gender %>";
                    </script>
                </div>
            </div>
            <% } else { %>
                
            <div class="card">
                <div class="card-header">
                    <div class="row">
                        <div class="col">Sample Data</div>
                        <div class="col">
                            <a href="/sample_data/add" class="btn btn-success btn-sm float-end">Add</a>
                        </div>
                    </div>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <tr>
                                <th>First Name</th>
                                <th>Last Name</th>
                                <th>Age</th>
                                <th>Gender</th>
                                <th>Action</th>
                            </tr>
                            <%
                            if(sampleData.length > 0)
                            {
                                sampleData.forEach(function(data){
                            %>
                            <tr>
                                <td><%= data.first_name %></td>
                                <td><%= data.last_name %></td>
                                <td><%= data.age %></td>
                                <td><%= data.gender %></td>
                                <td>
                                    <a href="/sample_data/edit/<%= data.id %>" class="btn btn-primary btn-sm">Edit</a>
                                </td>
                            </tr>
                            <%
                                });
                            }
                            else
                            {
                            %>
                            <tr>
                                <td colspan="5">No Data Found</td>
                            </tr>
                            <%
                            }
                            %>
                        </table>
                    </div>
                </div>
            </div>

            <% } %>

        </div> 

        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
</html>


```
Next go to the **routes/sample_data.js**  file and under this file, create a route to handle the edit form, data request to edit the data. Under this route, execute the update data query and after updating the data it will redirect to web page on which we display the MySQL data in the html table format.

**routes/sample_data.js**

```
var express = require('express');
var router = express.Router();
var database = require('../database');

router.get("/", function(request, response, next){

	var query = "SELECT * FROM sample_data ORDER BY id DESC";

	database.query(query, function(error, data){

		if(error)
		{
			throw error; 
		}
		else
		{
			response.render('sample_data', {title:'Node.js MySQL CRUD Application', action:'list', sampleData:data});
		}
	});
});

router.get("/add", function(request, response, next){

	response.render("sample_data", {title:'Insert Data into MySQL', action:'add'});

});

router.post("/add_sample_data", function(request, response, next){

	var first_name = request.body.first_name;
	var last_name = request.body.last_name;
	var age = request.body.age;
	var gender = request.body.gender;

	var query = `
	INSERT INTO sample_data 
	(first_name, last_name, age, gender) 
	VALUES ("${first_name}", "${last_name}", "${age}", "${gender}")
	`;
	database.query(query, function(error, data){

		if(error)
		{
			throw error;
		}	
		else
		{
			response.redirect("/sample_data");
		}
	});
});
router.get('/edit/:id', function(request, response, next){
	var id = request.params.id;
	var query = `SELECT * FROM sample_data WHERE id = "${id}"`;

	database.query(query, function(error, data){

		response.render('sample_data', {title: 'Edit MySQL Table Data', action:'edit', sampleData:data[0]});

	});
});
router.post('/edit/:id', function(request, response, next){

	var id = request.params.id;
	var first_name = request.body.first_name;
	var last_name = request.body.last_name;
	var age = request.body.age;
	var gender = request.body.gender;

	var query = `
	UPDATE sample_data 
	SET first_name = "${first_name}", 
	last_name = "${last_name}", 
	age = "${age}", 
	gender = "${gender}" 
	WHERE id = "${id}"
	`;
	database.query(query, function(error, data){

		if(error)
		{
			throw error;
		}
		else
		{
			response.redirect('/sample_data');
		}
	});
});
module.exports = router;

```

# Step 10 - Delete Data from MySQL table in Node.js Express Application with button

To Delete or Remove data from the table, create a Delete button in each row of data. Open  **views/sample\_data.ejs**  file and create a delete button which will display alongside the MySQL data in the HTML table format.

**views/sample\_data.ejs**

```
<!doctype html>
<html lang="en">
    <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <!-- Bootstrap CSS -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

        <title></title>
    </head>
    <body>
        <div class="container">
            <h1 class="text-center mt-3 mb-3"><%= title %></h1>
            
            <% if(action == 'add') { %>

            <div class="card">
                <div class="card-header">Sample Form</div>
                <div class="card-body">
                    <form method="POST" action="/sample_data/add_sample_data">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>First Name</label>
                                    <input type="text" name="first_name" id="first_name" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Last Name</label>
                                    <input type="text" name="last_name" id="last_name" class="form-control" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Age</label>
                                    <input type="number" name="age" id="age" class="form-control" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Gender</label>
                                    <select name="gender" class="form-control">
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="mb-3">
                            <input type="submit" name="submit_button" class="btn btn-primary" value="Add" />
                        </div>
                    </form>
                </div>
            </div>

            <% } else if(action == 'edit') { %>
            <div class="card">
                <div class="card-header">Sample Form</div>
                <div class="card-body">
                    <form method="POST" action="/sample_data/edit/<%= sampleData.id %>">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>First Name</label>
                                    <input type="text" name="first_name" id="first_name" class="form-control" value="<%= sampleData.first_name %>" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Last Name</label>
                                    <input type="text" name="last_name" id="last_name" class="form-control" value="<%= sampleData.last_name %>" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Age</label>
                                    <input type="number" name="age" id="age" class="form-control" value="<%= sampleData.age %>" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="mb-3">
                                    <label>Gender</label>
                                    <select name="gender" id="gender" class="form-control">
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="mb-3">
                            <input type="submit" name="submit_button" class="btn btn-primary" value="Edit" />
                        </div>
                    </form>
                    <script>
                    document.getElementById('gender').value="<%= sampleData.gender %>";
                    </script>
                </div>
            </div>
            <% } else { %>
                
            <div class="card">
                <div class="card-header">
                    <div class="row">
                        <div class="col">Sample Data</div>
                        <div class="col">
                            <a href="/sample_data/add" class="btn btn-success btn-sm float-end">Add</a>
                        </div>
                    </div>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <tr>
                                <th>First Name</th>
                                <th>Last Name</th>
                                <th>Age</th>
                                <th>Gender</th>
                                <th>Action</th>
                            </tr>
                            <%
                            if(sampleData.length > 0)
                            {
                                sampleData.forEach(function(data){
                            %>
                            <tr>
                                <td><%= data.first_name %></td>
                                <td><%= data.last_name %></td>
                                <td><%= data.age %></td>
                                <td><%= data.gender %></td>
                                <td>
                                    <a href="/sample_data/edit/<%= data.id %>" class="btn btn-primary btn-sm">Edit</a>
                                    <a href="/sample_data/delete/<%= data.id %>" class="btn btn-danger btn-sm">Delete</a>
                                </td>
                            </tr>
                            <%
                                });
                            }
                            else
                            {
                            %>
                            <tr>
                                <td colspan="5">No Data Found</td>
                            </tr>
                            <%
                            }
                            %>
                        </table>
                    </div>
                </div>
            </div>

            <% } %>

        </div> 

        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    </body>
</html>

```
After creating the delete button in each row of data, create the route for handling the delete data request. In that route, create one delete data query which will get the primary key value from the URL and based on that value it will delete data from MySQL table. It will redirect the web page to another url which will display the remaining data on the web page in HTML table format.

**routes/sample\_data.js**
```
var express = require('express');
var router = express.Router();
var database = require('../database');

router.get("/", function(request, response, next){

	var query = "SELECT * FROM sample_data ORDER BY id DESC";

	database.query(query, function(error, data){

		if(error)
		{
			throw error; 
		}
		else
		{
		response.render('sample_data', {title:'Node.js MySQL CRUD Application', action:'list', sampleData:data});
		}
	});
});
router.get("/add", function(request, response, next){

	response.render("sample_data", {title:'Insert Data into MySQL', action:'add'});
});
router.post("/add_sample_data", function(request, response, next){

	var first_name = request.body.first_name;
	var last_name = request.body.last_name;
	var age = request.body.age;
	var gender = request.body.gender;

	var query = `
	INSERT INTO sample_data 
	(first_name, last_name, age, gender) 
	VALUES ("${first_name}", "${last_name}", "${age}", "${gender}")
	`;
	database.query(query, function(error, data){

		if(error)
		{
			throw error;
           	}	
		else
		{
			response.redirect("/sample_data");
		}
	});
});
router.get('/edit/:id', function(request, response, next){

	var id = request.params.id;
	var query = `SELECT * FROM sample_data WHERE id = "${id}"`;

	database.query(query, function(error, data){
		
          response.render('sample_data', {title: 'Edit MySQL Table Data', action:'edit', sampleData:data[0]});

	});

});
router.post('/edit/:id', function(request, response, next){

	var id = request.params.id;
	var first_name = request.body.first_name;
	var last_name = request.body.last_name;
	var age = request.body.age;
	var gender = request.body.gender;

	var query = `
	UPDATE sample_data 
	SET first_name = "${first_name}", 
	last_name = "${last_name}", 
	age = "${age}", 
	gender = "${gender}" 
	WHERE id = "${id}"
	`;

	database.query(query, function(error, data){

		if(error)
		{
			throw error;
		}
		else
		{
			response.redirect('/sample_data');
		}
	});

});
router.get('/delete/:id', function(request, response, next){

	var id = request.params.id; 
	var query = `DELETE FROM sample_data WHERE id = "${id}"`;

	database.query(query, function(error, data){

		if(error)
		{
			throw error;
		}
		else
                                             {
			response.redirect("/sample_data");
		}
	});
});
module.exports = router;

```

**Enjoy your CRUD NodeJs Express Application which uses EJS.**

51