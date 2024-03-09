# HTTP
http is a node js default module 

Read from 

1. https://www.w3schools.com/nodejs/nodejs_http.asp
2. https://nodejs.org/api/http.html
3. https://www.javascripttutorial.net/nodejs-tutorial/nodejs-http-module/
4. https://www.w3resource.com/node.js/nodejs-http-server.php
5. https://codeforgeek.com/node-js-https/


In Node.js, the http module is a core module that provides functionality to create HTTP servers and clients. It allows you to interact with the HTTP protocol, making it possible to handle incoming HTTP requests and outgoing HTTP responses.

HTTP is a object like entity having different methods for different use.

## 1. http.createServer:- 
This method is used to create an http server by using pure node js.

The http.createServer() method is used to create an HTTP server instance. It takes a callback function as an argument, which is executed whenever a request is received by the server.

In this callback function we pass two parameters first is request and second is response. 

Inside the callback function, you can define how the server should respond to incoming requests by setting headers, writing the response body, etc.


```node

const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});//define the type of respinse data
  res.end('Hello, World!');//response to the request with this data
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});


```
res.end:- is very important to make a successfull communication with res and req cycle.
Every time you write the localhost:3000 into your browser your brower by default make a GET request , and this req is received by our server that we created and response is send to the browser by the server. 

You can access information about the incoming request such as URL, HTTP method, headers, etc., from the request object and send the response using the response object.
Means we can get the proper detail of the request which is in the form of object like req URL, its method and header and can send the data to the frentend by using the same format.

## 2. HTTP method:- 

The HTTP methods like GET, POST, PUT, DELETE, etc., can be handled by checking the request.method property inside the request handler.

Based on the method, you can implement different logic for handling different types of requests

```node

const http = require('http');

const server = http.createServer((req, res) => {
    // Handling GET request
    if (req.method === 'GET') {
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end('GET request received');
    }
    // Handling POST request
    else if (req.method === 'POST') {
        let requestBody = '';

        req.on('data', (chunk) => {
            requestBody += chunk.toString();
        });

        req.on('end', () => {
            console.log('POST request body:', requestBody);
            res.writeHead(200, {'Content-Type': 'text/plain'});
            res.end('POST request received');
        });
    }
    // Handling PUT request
    else if (req.method === 'PUT') {
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end('PUT request received');
    }
    // Handling DELETE request
    else if (req.method === 'DELETE') {
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end('DELETE request received');
    }
    // Handling unsupported methods
    else {
        res.writeHead(405, {'Content-Type': 'text/plain'});
        res.end('Method Not Allowed');
    }
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});


```

For a GET request, it responds with a simple message.
For a POST request, it collects the request body, logs it to the console, and then responds.
For PUT and DELETE requests, it responds with simple messages.
If the request method is not supported (i.e., not GET, POST, PUT, or DELETE), it responds with a "Method Not Allowed" status code.






