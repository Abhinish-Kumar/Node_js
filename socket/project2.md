## server

```javascript
const express = require("express");
const http = require("http");
const socketIo = require("socket.io");
const cors = require("cors");

// Create an Express app
const app = express();

// Enable CORS for all origins (or specify particular domains if needed)
app.use(cors()); // This allows all origins by default

// Create HTTP server and bind it to the Express app
const server = http.createServer(app);

// Create Socket.IO instance and attach it to the HTTP server
const io = socketIo(server, {
  cors: {
    origin: "*", // Allow all origins (you can replace "*" with a specific domain like 'http://localhost:3000')
    methods: ["GET", "POST"], // Allow these HTTP methods
    allowedHeaders: ["my-custom-header"], // Optional: if you have custom headers
    credentials: true, // Allow credentials like cookies to be sent
  },
});

// Serve a simple HTML file (index.html) to the client
app.get("/", (req, res) => {
  res.sendFile(__dirname + "/index.html"); // Serve index.html when client visits root
});

// Listen for client connections
io.on("connection", (socket) => {
  console.log("A user connected"); //print on server

  // Handle incoming 'chat message' events from the client
  //user can send the data from frontend with this event
  socket.on("chat message", (msg) => {
    console.log("Message from client: " + msg);
    // Broadcast the message to all clients
    //wen we get the message from one client then we broadcast it to all the user
    io.emit("chat message", msg);
  });

  // Handle disconnection
  socket.on("disconnect", () => {
    console.log("A user disconnected");
  });
});

// Start the server on port 3000
server.listen(3000, () => {
  console.log("Server is running on http://localhost:3000");
});

```


```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Socket.IO Client</title>
    <!-- Include the Socket.IO client library -->
    <script src="https://cdn.socket.io/4.0.1/socket.io.min.js"></script>
  </head>
  <body>
    <h1>Socket.IO Chat</h1>
    <input type="text" id="message" placeholder="Type a message..." />
    <button onclick="sendMessage()">Send</button>

    <ul id="messages"></ul>

    <script>
      // Connect to the Socket.IO server
      //make connection to that socketserver
      //socket here is a new connection or a new user
      const socket = io("http://localhost:3000");

      // Listen for 'chat message' events from the server
      socket.on("chat message", (msg) => {
        // Append the message to the list
        let item = document.createElement("li");
        item.textContent = msg;
        document.getElementById("messages").appendChild(item);
      });

      // Send message to the server when the button is clicked
      function sendMessage() {
        let message = document.querySelector("#message").value;
        socket.emit("chat message", message); // Emit message to the server
        console.log("Message sent:", message); // Log the message
        document.querySelector("#message").value = ""; // Clear the input field
      }
    </script>
  </body>
</html>

```
