# HTTP
http is a node js default module 

In Node.js, the http module is a core module that provides functionality to create HTTP servers and clients. It allows you to interact with the HTTP protocol, making it possible to handle incoming HTTP requests and outgoing HTTP responses.

HTTP is a object like entity having different methods for different use.

1. http.createServer:- This method is used to create an http server by using pure node js.

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












