> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

#### 27. [Getting data from the request object - forms and cookies](#27)

#### 28. [Getting data from the query string](#28)

#### 29. [Getting data from params (URL wildcards) - req.params and req.param()](#29)

#### 30. [Sending files, and headers already sent!](#30)

#### 31. [The Router](#31)

#### 32. [The Express Generator](#32)

#### 33. [STOP - Checklist Update and Short Review](#33)

#### 34. [Don't fear the HTTP headers!!](#34)

---

<br>

### 27. Getting data from the request object - forms and cookies<a id="27"></a>

- In 06 Section Express 301- Req & Res revisited/express301/loginSite.js
- How to redirect user from post route by using [res.redirect()](https://expressjs.com/en/api.html#res.redirect) method after data submission
- How to save data using cookie by [res.cookie()](https://expressjs.com/en/api.html#res.cookie) method
- How to clear cookie data by [ res.clearCookie ?](https://expressjs.com/en/api.html#res.clearCookie)
- How to remove cookie data from chrom

<img src="notes/1%20how%20to%20delete%20cookie%20data.png" width="700">

```js
const path = require("path");

const express = require("express");
const app = express();

const cookieParser = require("cookie-parser");

const helmet = require("helmet");
app.use(helmet());

app.use(express.static("public"));
//for any data that comes in will be add in req.body
app.use(express.json());
//for any data that comes in will be add in req.body
app.use(express.urlencoded());

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));

app.get("/", (req, res, next) => {
  res.send("Sanity Check");
});

app.listen(3000);
console.log("Server listening on port 3000...");
```

- Change to current working dir and run cmd

```sh
npm init
npm install express --save
npm install ejs --save
npm install helmet --save
npm install cookie-parser --save
nodemon loginSite.js

```

---

- In 06 Section/express301/loginSite.js,

```js
const path = require("path");

const express = require("express");
const app = express();

const cookieParser = require("cookie-parser");

const helmet = require("helmet");
app.use(helmet());

app.use(express.static("public"));
//for any data that comes in will be add in req.body
app.use(express.json());
//for any data that comes in will be add in req.body
app.use(express.urlencoded());
app.use(cookieParser());

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));

app.get("/", (req, res, next) => {
  res.send("Sanity Check");
});

app.get("/login", (req, res, next) => {
  res.render("login");
});

// this route purpose is to only submit data, you will never see it on browser
app.post("/process_login", (req, res, next) => {
  // req.body is made by urlencoded, which parses the http message for sent data!
  const password = req.body.password;
  const username = req.body.username;

  // check the db to see if user credentials are valid
  // if they are valid...
  // - save their username in a cookie
  // - is send them to the welcome page
  if (password === "x") {
    // res.cookie takes 2 args:
    // 1. name of the cookie
    // 2. value to set it to
    res.cookie("username", username);

    // res.redirect takes 1 arg:
    // 1. Where to send the brower
    res.redirect("/welcome");
  } else {
    // The "?" is a special character in a URL
    res.redirect("/login?msg=fail&test=hello");
  }
  // res.json(req.body)
});

app.get("/welcome", (req, res, next) => {
  // req.cookies object will have a property for every named cookie
  // that has been set.
  res.render("welcome", {
    username: req.cookies.username,
  });
});

app.get("/logout", (req, res, next) => {
  // res.clearCookie takes 1 arg:
  // 1. Cookie to clear (by name)
  res.clearCookie("username");
  res.redirect("/login");
});

app.listen(3000);
console.log("Server listening on port 3000...");
```

<br>

### 28. Getting data from the query string<a id="28"></a>

- In 06 Section/express301/loginSite.js,
- How to use [req.query ](https://expressjs.com/en/api.html#req.query) ?

```js
const path = require("path");

const express = require("express");
const app = express();

const cookieParser = require("cookie-parser");

const helmet = require("helmet");
app.use(helmet());

app.use(express.static("public"));
//for any data that comes in will be add in req.body
app.use(express.json());
//for any data that comes in will be add in req.body
app.use(express.urlencoded());
app.use(cookieParser());

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));

app.use((req, res, next) => {
  if (req.query.msg === "fail") {
    res.locals.msg = `Sorry. This username and password combinatino does not exist.`;
  } else {
    res.locals.msg = ``;
  }

  // Send me on to the next piece of middleware!
  next();
});

app.get("/", (req, res, next) => {
  res.send("Sanity Check");
});

app.get("/login", (req, res, next) => {
  // the req object has a query property in Express
  // req.query is an object, wiht a property of every key in the query string
  // The query string is where you put insecure data
  // console.log(req.query)
  const msg = req.query.msg;

  if (msg === "fail") {
    //run some other function...
  }
  res.render("login");
});

// this route purpose is to only submit data, you will never see it on browser
app.post("/process_login", (req, res, next) => {
  // req.body is made by urlencoded, which parses the http message for sent data!
  const password = req.body.password;
  const username = req.body.username;

  // check the db to see if user credentials are valid
  // if they are valid...
  // - save their username in a cookie
  // - is send them to the welcome page
  if (password === "x") {
    // res.cookie takes 2 args:
    // 1. name of the cookie
    // 2. value to set it to
    res.cookie("username", username);

    // res.redirect takes 1 arg:
    // 1. Where to send the brower
    res.redirect("/welcome");
  } else {
    // The "?" is a special character in a URL
    res.redirect("/login?msg=fail&test=hello");
  }
  // res.json(req.body)
});

app.get("/welcome", (req, res, next) => {
  // req.cookies object will have a property for every named cookie
  // that has been set.
  res.render("welcome", {
    username: req.cookies.username,
  });
});

app.get("/logout", (req, res, next) => {
  // res.clearCookie takes 1 arg:
  // 1. Cookie to clear (by name)
  res.clearCookie("username");
  res.redirect("/login");
});

app.listen(3000);
console.log("Server listening on port 3000...");
```

<br>

### 29. Getting data from params (URL wildcards) - req.params and req.param()<a id="29"></a>

- In 06 Section/express301/loginSite.js,
- [How to use req.params property](https://expressjs.com/en/4x/api.html#req.params)
- How to use [ req.params()](https://expressjs.com/en/4x/api.html#req.param)

```js
const path = require("path");

const express = require("express");
const app = express();

const cookieParser = require("cookie-parser");

const helmet = require("helmet");
app.use(helmet());

app.use(express.static("public"));
//for any data that comes in will be add in req.body
app.use(express.json());
//for any data that comes in will be add in req.body
app.use(express.urlencoded());
app.use(cookieParser());

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));

app.use((req, res, next) => {
  if (req.query.msg === "fail") {
    res.locals.msg = `Sorry. This username and password combinatino does not exist.`;
  } else {
    res.locals.msg = ``;
  }

  // Send me on to the next piece of middleware!
  next();
});

app.get("/", (req, res, next) => {
  res.send("Sanity Check");
});

app.get("/login", (req, res, next) => {
  // the req object has a query property in Express
  // req.query is an object, wiht a property of every key in the query string
  // The query string is where you put insecure data
  // console.log(req.query)
  const msg = req.query.msg;

  if (msg === "fail") {
    //run some other function...
  }
  res.render("login");
});

// this route purpose is to only submit data, you will never see it on browser
app.post("/process_login", (req, res, next) => {
  // req.body is made by urlencoded, which parses the http message for sent data!
  const password = req.body.password;
  const username = req.body.username;

  // check the db to see if user credentials are valid
  // if they are valid...
  // - save their username in a cookie
  // - is send them to the welcome page
  if (password === "x") {
    // res.cookie takes 2 args:
    // 1. name of the cookie
    // 2. value to set it to
    res.cookie("username", username);

    // res.redirect takes 1 arg:
    // 1. Where to send the brower
    res.redirect("/welcome");
  } else {
    // The "?" is a special character in a URL
    res.redirect("/login?msg=fail&test=hello");
  }
  // res.json(req.body)
});

app.get("/welcome", (req, res, next) => {
  // req.cookies object will have a property for every named cookie
  // that has been set.
  res.render("welcome", {
    username: req.cookies.username,
  });
});

// app.param() - takes 2 args:
// 1. param to look for in the route
// 2. the callback to run (with the usuals)
app.param("id", (req, res, next, id) => {
  console.log("Params called:", id);
  // if id has something to do with stories...
  // if id has something to do with blog...
  next();
});

// app.get('/user/:uid',...)
// app.get('/user/admin/:uid',...)
// app.get('/user/profile/:uid',...)

// in a route, anytime something has a : in front it is a wildcard!
// wildcard, will match anything in that slot
app.get("/story/:id", (req, res, next) => {
  // the req.params object always exists
  // it will have a property for each wildcard in the route
  res.send(`<h1>Story ${req.params.storyId}</h1>`);
  // res.send('<h1>Story 1</h1>')
});

// THIS WILL NEVER RUN, because it matches above (without next())
// app.get('/story/:blogId',(req, res, next)=>{
//     // the req.params object always exists
//     // it will have a property for each wildcard in the route
//     res.send(`<h1>Story ${req.params.storyId}</h1>`)
//     // res.send('<h1>Story 1</h1>')
// })

app.get("/story/:storyId/:link", (req, res, next) => {
  // the req.params object always exists
  // it will have a property for each wildcard in the route
  res.send(`<h1>Story ${req.params.storyId} - ${req.params.link}</h1>`);
  // res.send('<h1>Story 1</h1>')
});

// --- Hard to manage ---
// app.get('/story/1',(req, res, next)=>{
//     res.send('<h1>Story 1</h1>')
// })

// app.get('/story/2',(req, res, next)=>{
//     res.send('<h1>Story 2</h1>')
// })

// app.get('/story/3',(req, res, next)=>{
//     res.send('<h1>Story 3</h1>')
// })

app.get("/logout", (req, res, next) => {
  // res.clearCookie takes 1 arg:
  // 1. Cookie to clear (by name)
  res.clearCookie("username");
  res.redirect("/login");
});

app.listen(3000);
console.log("Server listening on port 3000...");
```

<br>

### 30. Sending files, and headers already sent!<a id="30"></a>

- In 06 Section/express301/loginSite.js,

```js
const path = require("path");

const express = require("express");
const app = express();

const cookieParser = require("cookie-parser");

const helmet = require("helmet");
app.use(helmet());

app.use(express.static("public"));
//for any data that comes in will be add in req.body
app.use(express.json());
//for any data that comes in will be add in req.body
app.use(express.urlencoded());
app.use(cookieParser());

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));

app.use((req, res, next) => {
  if (req.query.msg === "fail") {
    res.locals.msg = `Sorry. This username and password combinatino does not exist.`;
  } else {
    res.locals.msg = ``;
  }

  // Send me on to the next piece of middleware!
  next();
});

app.get("/", (req, res, next) => {
  res.send("Sanity Check");
});

app.get("/login", (req, res, next) => {
  // the req object has a query property in Express
  // req.query is an object, wiht a property of every key in the query string
  // The query string is where you put insecure data
  // console.log(req.query)
  const msg = req.query.msg;

  if (msg === "fail") {
    //run some other function...
  }
  res.render("login");
});

// this route purpose is to only submit data, you will never see it on browser
app.post("/process_login", (req, res, next) => {
  // req.body is made by urlencoded, which parses the http message for sent data!
  const password = req.body.password;
  const username = req.body.username;

  // check the db to see if user credentials are valid
  // if they are valid...
  // - save their username in a cookie
  // - is send them to the welcome page
  if (password === "x") {
    // res.cookie takes 2 args:
    // 1. name of the cookie
    // 2. value to set it to
    res.cookie("username", username);

    // res.redirect takes 1 arg:
    // 1. Where to send the brower
    res.redirect("/welcome");
  } else {
    // The "?" is a special character in a URL
    res.redirect("/login?msg=fail&test=hello");
  }
  // res.json(req.body)
});

app.get("/welcome", (req, res, next) => {
  // req.cookies object will have a property for every named cookie
  // that has been set.
  res.render("welcome", {
    username: req.cookies.username,
  });
});

// app.param() - takes 2 args:
// 1. param to look for in the route
// 2. the callback to run (with the usuals)
app.param("id", (req, res, next, id) => {
  console.log("Params called:", id);
  // if id has something to do with stories...
  // if id has something to do with blog...
  next();
});

// app.get('/user/:uid',...)
// app.get('/user/admin/:uid',...)
// app.get('/user/profile/:uid',...)

// in a route, anytime something has a : in front it is a wildcard!
// wildcard, will match anything in that slot
app.get("/story/:id", (req, res, next) => {
  // the req.params object always exists
  // it will have a property for each wildcard in the route
  res.send(`<h1>Story ${req.params.storyId}</h1>`);
  // res.send('<h1>Story 1</h1>')
});

// THIS WILL NEVER RUN, because it matches above (without next())
// app.get('/story/:blogId',(req, res, next)=>{
//     // the req.params object always exists
//     // it will have a property for each wildcard in the route
//     res.send(`<h1>Story ${req.params.storyId}</h1>`)
//     // res.send('<h1>Story 1</h1>')
// })

app.get("/story/:storyId/:link", (req, res, next) => {
  // the req.params object always exists
  // it will have a property for each wildcard in the route
  res.send(`<h1>Story ${req.params.storyId} - ${req.params.link}</h1>`);
  // res.send('<h1>Story 1</h1>')
});

// --- Hard to manage ---
// app.get('/story/1',(req, res, next)=>{
//     res.send('<h1>Story 1</h1>')
// })

// app.get('/story/2',(req, res, next)=>{
//     res.send('<h1>Story 2</h1>')
// })

// app.get('/story/3',(req, res, next)=>{
//     res.send('<h1>Story 3</h1>')
// })

app.get("/logout", (req, res, next) => {
  // res.clearCookie takes 1 arg:
  // 1. Cookie to clear (by name)
  res.clearCookie("username");
  res.redirect("/login");
});

app.listen(3000);
console.log("Server listening on port 3000...");
```

<br>

### 31. The Router<a id="31"></a>

<br>

### 32. The Express Generator<a id="32"></a>

<br>

### 33. STOP - Checklist Update and Short Review<a id="33"></a>

<br>

### 34. Don't fear the HTTP headers!!<a id="34"></a>

<br>

---

38. <br>
    <br>

---

---

9. How to use [express.Router() ](https://expressjs.com/en/4x/api.html#express.router) for creating micro routes<br>
   <br>
   <br>

10. How to use [diff. routher methods](https://expressjs.com/en/4x/api.html#router) ?<br>
    <br>
    <br>

11. Router file layout

- We bring in the Router
- We use the Router with get, post, all, etc method
- We export the Router
  <br>
  <br>

---

12. How to download Bank-statement-Image.png from hyperlink, inside userStatement

- [res.download](https://expressjs.com/en/api.html#res.download) - takes 3 args:
- 1 path
- 2 (optional) what you want to call the file when the user gets it
- 3 (optional) callback (which accepts an error)

```
app.get("/statement", (req, res, next) => {

  res.download(
    path.join(__dirname, "userStatements/BankStatementChequing.png"),

    "jimsStatement.png",

    (err) => {
      console.log(err);
    }
  );
```

<img src="notes/10%20click%20on%20download%20link.png" width="700">
<br>
<img src="notes/10%20download.png" width="700">
<br>
<br>

13. How to render Bank-statement-Image.png on browser from hyperlink, located in userStatement folder

- sendFile will load in the browser!

```
app.get("/statement", (req, res, next) => {

  res.sendFile(path.join(__dirname, 'userStatements/BankStatementChequing.png'),'jimsStatement.png')

});
```

<img src="notes/12%20render%20on%20browser.png" width="700">
<br>
<br>

13. [How to use express generator ?](https://expressjs.com/en/starter/generator.html)<br>
    <br>
    <br>

14. How to do empty cahce and Hard reseting by opening dev tools<br>
    <img src="notes/2%20How%20to%20do%20empty%20cache%20and%20hard%20resting.png" width="700">
    <br>
    <br>

---

16. What are [http headers ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) ?

- Different res. methods to transfer http message

  - <img src="notes/13%20res%20method%20on%20express.png" width="700">

- Express server is doing some behind the scene work so what we are not doing

  - <img src="notes/14%20what%20we%20are%20not%20doing%20.png" width="700">

- Express server send http message to browser

  - <img src="notes/15%20HTTP%20message.png" width="700">

- Process of Http message transfering
- <img src="notes/16%20connection%20bw%20clent%20and%20server.png" width="700">

<br>
<br>

16. How to makes notes<br>
    <img src="notes/3%20How%20to%20write%20docx.png" width="700">
    <br>
    <br>

# Notice

- Post route its only purpose is for user to submit data, we accept the data then we send them to where they actually belong
  -We do redirecting after post request
- Cookie: The data(username) is stored on browser,and browser will send it out to server every time a request is made
- we save Cookie inside post route: save their username in a cookie
- Session: The data is stored on server, and the browser give key for that data
- An anchor tag i,e href, always point to get route
- Router file layout
  - We bring in the Router
  - We use the Router with get, post, all, etc method
  - We export the Router (to app.use() as middle ware)
