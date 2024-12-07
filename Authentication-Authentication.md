# Authentication and Authorization in Node.js

## 1. Middleware

Middleware in Node.js is a function that intercepts and processes incoming requests and outgoing responses during the request-response cycle in an application.
Middleware is a phase where number of functions executes.

or 

Middleware is like a series of tasks that happen behind the scenes in a web appliaction, It is a way to add extra functionality to your application's request-response cycle. Such as  logging ,authentication checks or modifying request data. before it reaches its final destination. 

### What Middleware Can Do:
1. **Modify Requests or Responses**: Middleware can tweak request or response objects before passing them further.
2. **Execute Code**: It can execute any required logic at specific points in the cycle.
3. **Control Flow**: Middleware decides whether to pass control to the next middleware or terminate the request-response cycle.
4. **Handle Errors**: Middleware is often used for centralized error handling.

### Syntax:
```javascript
app.use((req, res, next) => {
  console.log('Middleware executed!');
  next(); // Pass control to the next middleware
});
```

### Key Characteristics of Middleware:
1. **Sequential Execution**: Middleware functions are executed in the order they are defined.
2. **Versatile Use Cases**:
   - Logging.
   - Authentication and Authorization.
   - Parsing request bodies (e.g., using `body-parser`).
   - Serving static files (e.g., `express.static`).
   - Error handling.

### General Characteristics of Middleware:
1. **Intermediary Role**: Middleware acts as a bridge between two systems (e.g., an application and a database). It ensures the incoming request is authorized and then provides access to the required data.
2. **Enhances Functionality**: Middleware adds features like security, logging, data transformation, and session management without modifying the core application.
3. **Database Access**: Middleware manages and interfaces interactions with databases or data warehouses efficiently.

### Real-World Analogy:
Think of middleware as a manager or a gatekeeper. It evaluates every request coming into the system, authorizes it, and then allows access to the data or functionality if the request is valid.


1. Request phase :- asking for some data from database or server.
2. Middleware phase :- when server listen to the request first it sends the incoming request to the series of functions called middleware that checks your request and then check their database or in record thta is this user a valid user or not if the user is valid user then , it runs next() so that you reach to the actual resource or required resource and you are not a valid user it simply run a function that will give a error message that the person is not a authorized one.
3.  Final response phase :- aftert passing through the middleware ,your request processed and the system sends back a response. it could be the menu you requested or confirmation of your reservation.


Note :- authorization  and authentication are done at the middleware phase.

4. Why we use next() function in middleware function :- it tells express that the current middleware is completely processed. then it will give access to the server.
5. app.use() :- tells express js to run this first becasue it is  a middleware. 

examples of middleware :- body-parsing , authentication,router. 

## real world example

```javascript

const express = require("express");
const app = express();

let user = "Abhish";
let password = 12345;

let logRequest = (req, res, next) => {
  if (user == "Abhinish" && password == 12345) {
    next();
  } else {
    res.end("You are not a valid user");
  }
};

app.get("/", logRequest, (req, res) => {
  res.end("hello user you are a valid user ");
});

app.listen(4400, () => {
  console.log("Your server is running at port 4400");
});

```

This is the simplest and best example of middleware. You can validate user.


## example 2 show time of user enter with url

```javascript
const express = require("express");
const app = express();

let user = "Abhish";
let password = 12345;

let logRequest = (req, res, next) => {
  //it will show the timing of user when enter in your site
  console.log(new Date().toLocaleString() + "     " + req.originalUrl);
  if (user == "Abhinish" && password == 12345) {
    next();
  } else {
    res.end("You are not a valid user");
  }
};

app.get("/", logRequest, (req, res) => {
  res.end("hello user you are a valid user ");
});

app.listen(4400, () => {
  console.log("Your server is running at port 4400");
});


```


## example 

If we want to add middleware for every route 

```javascript

const express = require("express");
const app = express();

let user = "Abhish";
let password = 12345;

let logRequest = (req, res, next) => {
  //it will show the timing of user when enter in your site
  console.log(new Date().toLocaleString() + "     " + req.originalUrl);
  if (user == "Abhinish" && password == 12345) {
    next();
  } else {
    res.end("You are not a valid user");
  }
};

app.use(logRequest);

app.get("/", (req, res) => {
  res.end("hello user you are a valid user ");
});

app.listen(4400, () => {
  console.log("Your server is running at port 4400");
});

```

It will give us every route.


Note:- you can use this middleware to create public or protected route ,eg :- portfolio is  a personal route :- first you have to check that user exist or not then you give the portfolio information. and songs are public route where any one can access the song without any authentication. 


If you want that no one can access any of your route then , you can apply middleware to all the routes, and you provide the login page to login first before use of the appliaction.


# Chapter 2

Imagine you are the manager of the "hotel" appliaction, and you want to ensure that only authorized staff members can access certain fetures. This is where authentication comes in. 

## 1. Verifying Identity (Authentication) :

- Scenario :- write password and name then you are authorized.

## Access Control (Authorization) :

- controls that a person has over resources.


## Which we implement first Authentication or authorization

1. First we authorize the person
2. Then we give authority of resources.



when we make request to server , middleware extract the username and password and check for a valid user , if its a valid user then it will give , access to the server otherwise , it will show error message.

We store usernam and password in our system.



























