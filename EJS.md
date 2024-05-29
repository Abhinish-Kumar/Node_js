# EJS 
EJS(Embedded JavaScript) is a simple templating language that lets you generate HTML markup with plain JavaScript. It's commonly used with Node.js to create dynamic web pages by embedding JavaScript logic within HTML templates. 

### Key Features of EJS
1. Embedded JavaScript: EJS allows you to embed JavaScript code directly within HTML using <% %> delimiters.
2. Variables: You can inject variables into the template using <%= %>
3. Control Flow: You can use JavaScript control structures (like if statements, loops) within the template.
4. Partial Views: EJS supports partials, allowing you to include reusable pieces of HTML in multiple templates.
5. Layout Templates: EJS can be used to define layouts, making it easier to maintain consistent design across multiple pages.


### Setting Up EJS in a Node.js Application

#### Installing EJS

```javascript
npm install ejs
```

#### Configuring EJS in an Express Application

```nodejs

const express = require('express');
const app = express();

// Set EJS as the templating engine
app.set('view engine', 'ejs');

// Define a route
app.get('/', (req, res) => {
  res.render('index', { title: 'Welcome', message: 'Hello there!' });
});

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});


```

#### Creating EJS Templates

Create a directory named views (or another directory as specified) in your project root. Inside this directory, create an EJS file, e.g., index.ejs:

```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
</head>
<body>
  <h1><%= message %></h1>
  <p>This is a sample EJS template.</p>
</body>
</html>


```


### Example Application Structure

```javascript

my-app/
│
├── views/
│   ├── index.ejs
│   └── partials/
│       └── header.ejs
│
├── app.js
├── package.json
└── package-lock.json


```


## Exercise

```nodejs

const express = require('express');
const app = express();

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
  const data = {
    title: 'EJS Example',
    message: 'Hello from EJS!',
    items: ['Item 1', 'Item 2', 'Item 3']
  };
  res.render('index', data);
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

```

```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title><%= title %></title>
</head>
<body>
  <%- include('partials/header') %>
  <h1><%= message %></h1>
  <ul>
    <% items.forEach(item => { %>
      <li><%= item %></li>
    <% }); %>
  </ul>
</body>
</html>

```



# Template Engine

A template engine is a software component used in web development to generate dynamic web pages. It enables developers to combine HTML templates with dynamic data to produce the final HTML content that is sent to the user's browser. Template engines are essential for separating the presentation layer (HTML) from the logic layer (business logic), making code easier to manage and maintain.

### Types of Template Engines

#### Server-Side Template Engines

1. EJS (Embedded JavaScript)
2. Pug (formerly Jade)
3. Handlebars
4. Thymeleaf

#### Client-Side Template Engines

1. Mustache
2. Handlebars
3. Angular
4. React JSX









