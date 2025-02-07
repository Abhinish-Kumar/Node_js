## Server

```javascript
// Import necessary modules
const http = require("http");
const socketIo = require("socket.io");

// Create an HTTP server
const server = http.createServer();

// Attach Socket.IO to the server with CORS configuration
const io = socketIo(server, {
  cors: {
    origin: "*", // Allows all origins (You can also specify specific domains like 'http://localhost:3000' instead of "*")
    methods: ["GET", "POST"], // Allowed methods
    allowedHeaders: ["my-custom-header"], // Optional: If you have custom headers
    credentials: true, // Allows cookies to be sent with requests
  },
});

// Define the port
const PORT = 3000;

// Start the server
server.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});

// Handle client connections
io.on("connection", (socket) => {
  console.log("A user connected with socket ID:", socket.id);

  // Send a message to the client
  socket.emit("message", "Hello from the server!");

  // Handle custom event "ready"
  socket.on("ready", () => {
    console.log("Client is ready");
  });

  // Handle the disconnection event
  socket.on("disconnect", () => {
    console.log("A user disconnected");
  });
});


## client

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
    <h1>Socket.IO Client</h1>

    <script>
      // Connect to the Socket.IO server
      const socket = io("http://localhost:3000");

      // Emit "ready" event when the client is connected
      socket.emit("ready");

      // Listen for the "connect" event (when the client is connected)
      socket.on("connect", () => {
        console.log("Connected as " + socket.id);
      });

      // Listen for a custom message from the server
      socket.on("message", (data) => {
        console.log("Message from server:", data);
      });

      // Optionally listen for other events
      socket.on("disconnect", () => {
        console.log("Disconnected from the server");
      });
    </script>
  </body>
</html>

```

```
