```javascript
const express = require('express');
const app = express();

// Middleware to parse JSON bodies
app.use(express.json());

// Handle a GET request to demonstrate headers
app.get('/headers', (req, res) => {
  // Read headers from the request
  const userAgent = req.headers['user-agent']; // Example of reading from req
  const acceptHeader = req.headers['accept']; // Example of reading from req
  console.log('User-Agent:', userAgent);
  console.log('Accept Header:', acceptHeader);

  // Set headers in the response
  res.setHeader('X-Custom-Header', 'This is a custom header'); // Set custom response header
  res.setHeader('Cache-Control', 'max-age=3600'); // Set Cache-Control header

  // Respond back with JSON data and headers
  res.status(200).json({
    message: 'Headers processed and custom header set.',
    userAgent,
    acceptHeader,
  });
});

// Handle POST request with Authorization
app.post('/secure', (req, res) => {
  const authHeader = req.headers['authorization'];
  if (authHeader && authHeader.startsWith('Bearer ')) {
    const token = authHeader.split(' ')[1]; // Extract token
    if (token === 'mysecrettoken') {
      res.status(200).json({ message: 'Access granted' });
    } else {
      res.status(403).json({ message: 'Forbidden: Invalid token' });
    }
  } else {
    res.status(401).json({ message: 'Unauthorized: Missing token' });
  }
});

// Enable CORS (Cross-Origin Resource Sharing)
app.use((req, res, next) => {
  res.setHeader('Access-Control-Allow-Origin', '*'); // Allow all origins
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS'); // Allowed methods
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization'); // Allowed headers
  next();
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});

```



```javascript
const axios = require('axios');

// Function to send a GET request to the server and log the response
async function getHeaders() {
  try {
    const response = await axios.get('http://localhost:3000/headers', {
      headers: {
        'Accept': 'application/json',
        'User-Agent': 'Node.js Client',
      },
    });
    console.log('Response Data:', response.data);
    console.log('Response Headers:', response.headers);
  } catch (error) {
    console.error('Error:', error.message);
  }
}

// Function to send a POST request with Authorization header
async function postWithAuthorization() {
  try {
    const response = await axios.post('http://localhost:3000/secure', {}, {
      headers: {
        'Authorization': 'Bearer mysecrettoken',
      },
    });
    console.log('Response Data:', response.data);
  } catch (error) {
    console.error('Error:', error.message);
  }
}

// Call the functions
getHeaders();
postWithAuthorization();

```
