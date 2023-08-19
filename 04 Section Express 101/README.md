> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

#### 12. [What is Express and why should I care?](#12)

#### 13. [Enter Express... the basics](#13)

#### 14. [Basic Routing in Express](#14)

#### 15. [Serving Static Files in Express](#15)

<br>

### 12. What is Express and why should I care?<a id='12'></a>

- ref. [express](https://expressjs.com/)

<br>

### 13. Enter Express... the basics<a id='13'></a>

- In 04 Section Express/express101/1_expressServer.js
- run cmd to initalize package.json

```sh
npm init
npm i express --save
nodemon 1_expressServer
```

---

```js
// NODEJS IS the language
// Express is node, a node module

// http is a native module -old code
// const http = require('http'); -old code

// express is a 3rd party module
const express = require("express");

// An "app" is the express function (createAppliction inside the Express module)
// invoked and is an Express appliction
const app = express();

// all is a method, and it takes 2 args:
// 1. route
// 2. callback to run if the route is requested
app.all("*", (req, res) => {
  // Express handles the basic headers (status code, mime-type)! Awesome!
  res.send(`<h1>This is the home page</h1>`);
  // Express handles the end! Awesome!
});

app.listen(3000);
console.log("The server is listening on port 3000...");
```

<br>

### 14. Basic Routing in Express<a id='14'></a>

- In 04 Section Express/express101/2_expressRouting.js
- run cmd to initalize package.json

```sh
npm init
npm i express --save
nodemon 2_expressRouting
```

```js
const express = require("express");
const app = express();

// app object has a few methods:
// HTTP verbs! REST verbs!
// CRUD app cooresponence!
// 1. get - READ
// - DEFAULT for all browsers is get.
// 2. post - CREATE
// 3. delete - DELETE
// 4. put - UPDATE
// 5. all - i will accept any method

// Take 2 args:
// 1. path or route
// 2. callback to run if an HTTP request that matchs THIS verb
// is made to the path in #1
// app.all('/',(req,res)=>{
//     res.send(`<h1>Welcome to the home page!`)
// })

// Basic routing with diff. http method request
app.get("/", (req, res) => {
  console.log(req);
  res.send(`<h1>Welcome to the home GET page!`);
});

app.post("/", (req, res) => {
  res.send(`<h1>Welcome to the home POST page!`);
});

app.delete("/", (req, res) => {});

app.put("/", (req, res) => {});

app.listen(3000);
console.log("The server is listening on port 3000...");
```

---

- open postman and make get, post, delete, update http request on "http://localhost:3000/"

- ref. [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods "mdn")

<br>

### 15. Serving Static Files in Express<a id='15'></a>

<br>
