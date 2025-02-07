### server

```javascript
let users = 0;

io.on("connection", (socket) => {
  users++; // Increment user count
  console.log(`Id of a new user: ${socket.id}`);
  console.log(`Total connected users: ${users}`);

  socket.on("disconnect", () => {
    users--; // Decrement the user count when they disconnect
    console.log(`User with id ${socket.id} disconnected`);
    console.log(`Total connected users: ${users}`);
  });
});
```

client 

```javascript
 const socket = io("http://localhost:3000");//user connected
```


### server 
send data to all the user on connectection, when user triger greet event 

```javascript
let users = 0;

io.on("connection", (socket) => {
  users++; // Increment user count
  console.log(`Id of a new user: ${socket.id}`);
  console.log(`Total connected users: ${users}`);

  //emit message to all the connected user
  io.emit("greetUser", `Hello ${socket.id}`);

  socket.on("disconnect", () => {
    users--; // Decrement the user count when they disconnect
    console.log(`User with id ${socket.id} disconnected`);
    console.log(`Total connected users: ${users}`);
  });
});

```

client

```javascript
 const socket = io("http://localhost:3000");
      socket.on("greetUser", (greetData) => {
        console.log(greetData); //Output Hello 9aa5-0wFTY5Vcj-hAAAD
      });
```

### Server 

client send data to server and server print 


```javascript
let users = 0;

io.on("connection", (socket) => {
  users++; // Increment user count
  console.log(`Id of a new user: ${socket.id}`);
  console.log(`Total connected users: ${users}`);

  //emit message to all the connected user
  io.emit("greetUser", `Hello ${socket.id}`);

  socket.on("disconnect", () => {
    users--; // Decrement the user count when they disconnect
    console.log(`User with id ${socket.id} disconnected`);
    console.log(`Total connected users: ${users}`);
  });

  socket.on("clientGreet", (clientData) => {
    console.log(clientData);
  });
});
```

client 

```javascript
 //our client is clreated
      const socket = io("http://localhost:3000");
      socket.on("greetUser", (greetData) => {
        console.log(greetData);
      });

      socket.emit("clientGreet", "Hello Server");
```

### server

broadcast the users message to all the connected user

```javascript
let users = 0;

io.on("connection", (socket) => {
  users++; // Increment user count
  console.log(`Id of a new user: ${socket.id}`);
  console.log(`Total connected users: ${users}`);

  //emit message to all the connected user
  io.emit("greetUser", `Hello ${socket.id}`);
  socket.on("clientGreet", (clientData) => {
   io.emit("allUser",clientData);

  });

  socket.on("disconnect", () => {
    users--; // Decrement the user count when they disconnect
    console.log(`User with id ${socket.id} disconnected`);
    console.log(`Total connected users: ${users}`);
  });
});
```

```javascript
 //our client is clreated
      const socket = io("http://localhost:3000");
      socket.on("greetUser", (greetData) => {
        console.log(greetData);
      });

      socket.emit("clientGreet", "Hello Server");
      socket.on("allUser", (datafromserver) => {
        document.writeln("from server" + datafromserver);
      });
```





