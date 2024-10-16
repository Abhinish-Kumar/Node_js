# Cookie in Node js

```javascript
const express = require("express");
const cookieParser = require("cookie-parser");
const app = express();

app.use(cookieParser());

// Set cookie with options
app.get("/set-cookie", (req, res) => {
  res.cookie("myCookie", "hello", {
    httpOnly: true, // Prevents JavaScript access
    secure: true, // Ensures transmission over HTTPS
    sameSite: "strict", // Protects against CSRF attacks
    expires: new Date(Date.now() + 3600000), // Expires in 1 hour
  });
  res.send("Cookie set!");
});

// Get cookie
app.get("/get-cookie", (req, res) => {
  const cookieValue = req.cookies.myCookie;
  res.send(`Cookie value: ${cookieValue}`);
});

app.get("/logout", (req, res) => {
  res.clearCookie("myCookie");
  res.send("Logged out");
});

app.listen(3000, () => {
  console.log("Server listening on port 3000");
});

```
