```javascript
const express = require("express");
const path = require("path");
const cookieParser = require("cookie-parser");

const app = express();

// Middleware to parse JSON bodies
app.use(express.json());
app.use(cookieParser());

// Serve static files from the "public" directory
app.use(express.static(path.join(__dirname, "public")));

const users = [
  {
    username: "user",
    password: "123",
    id: 1,
    about:
      "you name  is a user and this is your secrete content that no body can hack your reading content this is realy top secrete",
  },
  {
    username: "admin",
    password: "admin123",
    id: 2,
    about: "you have nothing special to hide from other people ",
  },
];

// Login Endpoint
app.post("/login", (req, res) => {
  const { username, password } = req.body;

  // Validate input
  if (!username || !password) {
    return res
      .status(400)
      .json({ error: "Username and password are required." });
  }

  const user = users.find(
    (u) => u.username === username && u.password === password
  );

  if (user) {
    // Send user data on successful login
    res.cookie("name", user.username);
    res.cookie("password", user.password);
    res.json({
      success: true,
      message: "Login successful! from node js",
      data: user.about,
    });
  } else {
    // Send error message for invalid credentials
    res.status(401).json({
      success: false,
      message: "Invalid username or password. from node js ",
    });
  }
});

app.get("/dashboard", (req, res) => {
  let name = req.cookies.name;
  let password = req.cookies.password;
  console.log(name, password);
  const user = users.find(
    (u) => u.username === name && u.password === password
  );
  if (user) {
    res.send("welcome" + name);
  } else {
    res.send("first login");
  }
});

app.post("/register", (req, res) => {
  let { name, password, about } = req.body;
  console.log(req.body);
  let data = {
    username: name,
    password: password,
    id: 1,
    about: about,
  };
  users.push(data);
  res.send("successfully register");
});

app.get("/logout", (req, res) => {
  res.clearCookie("name");
  res.clearCookie("password");
  res.send("loged out");
});

// Handle undefined routes
app.use((req, res) => {
  res.status(404).json({ error: "Page not found." });
});

// Start the server
const PORT = 3000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));

```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Login</title>
    <style>
      #container {
        width: 400px;
        height: 400px;
        border: 2px solid grey;
      }
    </style>
  </head>
  <body>
    <h1>Register</h1>
    <form id="registerForm">
      <label for="nameReg">Username:</label>
      <input type="text" id="nameReg" name="nameReg" required /><br /><br />
      <label for="passwordReg">Password:</label>
      <input
        type="text"
        id="passwordReg"
        name="passwordReg"
        required
      /><br /><br />

      <label for="aboutReg">About:</label>
      <input type="text" id="aboutReg" name="aboutReg" required /><br /><br />
      <button type="submit">Registre</button>
    </form>
    <a href="/dashboard">dashboard</a>
    <a href="/logout">Loagout</a>
    <h1>Login</h1>
    <form id="loginForm">
      <label for="username">Username:</label>
      <input type="text" id="username" name="username" required /><br /><br />

      <label for="password">Password:</label>
      <input
        type="password"
        id="password"
        name="password"
        required
      /><br /><br />

      <button type="submit">Login</button>
    </form>

    <p id="message"></p>

    <div id="container">
      <p></p>
    </div>
    <script>
      //register
      document
        .getElementById("registerForm")
        .addEventListener("submit", async (e) => {
          e.preventDefault();
          const name = document.getElementById("nameReg").value;
          const password = document.getElementById("passwordReg").value;
          const about = document.getElementById("aboutReg").value;

          let response = await fetch("/register", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ name, password, about }),
          });
        });

      //login
      document
        .getElementById("loginForm")
        .addEventListener("submit", async (e) => {
          e.preventDefault();
          const username = document.getElementById("username").value;
          const password = document.getElementById("password").value;

          const response = await fetch("/login", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ username, password }),
          });
          let data = await response.json();
          const message = document.getElementById("message");
          if (response.ok) {
            console.log(data);
            message.textContent = data.message;
            message.style.color = "green";
            document.querySelector("#container p").textContent = data.data;
          } else {
            message.textContent = data.message;
            message.style.color = "red";
          }
        });
    </script>
  </body>
</html>

```
