> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

#### 16. [Middleware. (It's all Express really is.)](#16)

#### 17. [Putting on your Express helmet, and other awesome Express middleware](#17)

#### 18. [Responding with JSON](#18)

#### 19. [STOP - Time for a Review](#19)

#### 20. [Chose your weapon - API or server side rendering](#20)

#### 21. [Wiring up Express with a view engine](#21)

#### 22. [Note for next video](#22)

#### 23. [Rendering in Express (with EJS) - Part1 of 2](#23)

#### 24. [Rendering in Express (with EJS) - Part2 of 2](#24)

#### 25. [Rendering Engine Option 2. Handlebars](#25)

#### 26. [Rendering Engine Option 3: Pug/Jade](#26)

---

<br>

### 16. Middleware. (It's all Express really is.)<a id='16'></a>

- initialize package.json, install express, run server
  - because we move to new folder

```sh
npm init
npm install express --save
nodemon 1_appUse_video_16
```

---

- In 05 Section Express 201- Middleware and Rendering/express201/1_appUse_video_16.js

```js
const express = require("express");
const app = express();

// Express = 2 things
// 1. Router
// 2. Middleware that comprises a webframework

// Req ---MIDDLEWARE---> Res
// Middleware function is ANY function that has access to the req, res, next object.

// Req ---MIDDLEWARE---> Res
// 1. Request comes in.
// 2. We need to validate the user, sometimes.
// 3. We need to store some things in the DB.
// 4. If there is data from the user we need to parse it and store it
// 5. Res

function validateUser(req, res, next) {
  // get info out of the req object
  // do some stuff with the DB
  res.locals.validated = true;
  console.log("VALIDATED RAN!");
  next();
}

// This will run validateUser on ALL paths, all methods!
app.use(validateUser);

// this will run validateUser on /admin, all methods!
app.use("/admin", validateUser);

// this will run validateUser on /, only on get methods! And, by the way, it looks like this...
app.get("/", validateUser);

app.get("/", (req, res, next) => {
  res.send("<h1>Main Page</h1>");
  console.log(res.locals.validated);
});

app.get("/admin", (req, res, next) => {
  res.send("<h1>Admin Page</h1>");
  console.log(res.locals.validated);
});

app.listen(3000);
```

<br>

### 17. Putting on your Express helmet, and other awesome Express middleware<a id='17'></a>

- [helmet](https://www.npmjs.com/package/helmet)

  - to protect server from various attack

<br>

- [express.static('public')](https://expressjs.com/en/4x/api.html#express.static)

<br>

- [express.json()](https://expressjs.com/en/4x/api.html#express.json)

<br>

- [express.urlencoded({extended:false});](https://expressjs.com/en/4x/api.html#express.urlencoded)

---

- In 05 Section Express 201- Middleware and Rendering/express201/2_helmetAndOthers_vieo_17.js

```js
const express = require("express");
const app = express();
const helmet = require("helmet");

app.use(helmet());

app.use(express.static("public"));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

// 1. static
// 2. json
// 3. urlencoded

app.post("/ajax", (req, res) => {
  console.log(req.body);
  res.json(["Test", 1, 2, 3, 4]);
});

app.listen(3000);
```

<br>

### 18. Responding with JSON<a id='18'></a>

- Anytime we need to respond with json, we use [res.json()](https://expressjs.com/en/4x/api.html#res.json), not res.send - Anytime we need to respond with HTML, we use res.render()

- In 05 Section Express 201- Middleware and Rendering/express201/2_helmetAndOthers_vieo_17.js

- In postman make a post request on "localhost:3000/ajax" route
  - select xx-www-form-urlencoded
  - write "name: rob" in key value pair

<br>

### 19. STOP - Time for a Review<a id='19'></a>

<br>

### 20. Chose your weapon - API or server side rendering<a id='20'></a>

- What make up myspace server-concept<br>

<img src="notes/1%20server%20concept.png" width="700">

<br>

---

- Server side rendering VS APIs

<img src="notes/5%20choose%20ur%20weapon.png" width="700">

<img src="notes/2%20chose%20ur%20weapon.png" width="700">

<br>

---

- Working of Server side rendering<br>
  Building template every single time then sending to client<br>
  In server side rendering we can use cookies, session

- [My Space](https://myspace.com/discover/featured)

- [Wikipedia](https://en.wikipedia.org/wiki/Express.js)

<br>

<img src="notes/4%20server%20side%20rendering.png" width="700">

<img src="notes/6%20my%20space.png" width="700">

<br>

---

- Working of JSON APIs<br>
  Sending HTML,CSS,JS on first load, then update the DOM by JSON

- [Facebook](https://www.facebook.com/)

- [Amazon](https://www.amazon.com/)

<br>

<img src="notes/3%20JSON%20APIs.png" width="700">

<br>

### 21. Wiring up Express with a view engine<a id='21'></a>

<br>

### 22. Note for next video<a id='22'></a>

<br>

### 23. Rendering in Express (with EJS) - Part1 of 2<a id='23'></a>

- [ejs](https://ejs.co/)

- In 05 Section Express 201- Middleware and Rendering/express201/3_rendering_video_21.js

```js
// 1. Express as we know it happens. This File.
// 2. We define a view engine.
// - EJS
// - Mustache
// - Handlebars
// - Jade/Pug
// 3. Inside one of our routes, we have a res.render
// 4. We pass that res.render 2 things:
// - the file we want to use.
// - the data we want to send to that file
// 5. Express uses the node module for our specified view engine and parses the file.
// - that means, it takes the HTML/JS/CSS and combines it with whatever "node" there is in the file
// 6. The final result of this process is a compiled product of the things the browser can read.
// - HTML, JS, CSS.

const path = require("path");

const express = require("express");
const app = express();

const helmet = require("helmet");
app.use(helmet()); //MY BAD... HELMET ON... READY FOR BATTLE!

// serve up static files
app.use(express.static("public"));
// parse json and urlencoded data into req.body
app.use(express.json());
app.use(express.urlencoded());

// app.set(), takes 2 args:
// 1. key
// 2. value
app.set("view engine", "ejs"); // type of the file "ejs"
app.set("views", path.join(__dirname, "views")); // location of the file "machine path"

app.get("/", (req, res, next) => {
  res.render("index"); // name of the file "index"
});

app.listen(3000);
```

<br>

### 24. Rendering in Express (with EJS) - Part2 of 2<a id='24'></a>

- In 05 Section Express 201- Middleware and Rendering/express201/4_ejsPractice_video_23.js

```js

```

- [app.set()](https://expressjs.com/en/api.html#app.set)
- [res.render()](https://expressjs.com/en/api.html#res.render)
  <br>

### 25. Rendering Engine Option 2. Handlebars<a id='25'></a>

<br>

### 26. Rendering Engine Option 3: Pug/Jade<a id='26'></a>

<br>

35. View Engine concept: What is EJS templating, and how to [install the ejs](https://ejs.co/) module ?
    <br>
    <br>

36. , takes 2 args<br>

- 1.  key
- 2.  value
      <br>
      <br>

11. Overview of ejs setup

```
const path = require("path");

const express = require("express");
const app = express();

const helmet = require("helmet");
app.use(helmet());

// serve up static files
app.use(express.static("public"));

// parse json and urlencoded data into req.body
app.use(express.json());
app.use(express.urlencoded());

// type of the file "ejs"
app.set("view engine", "ejs");

// location of the file on "machine path"
app.set("views", path.join(__dirname, "views"));


app.get("/", (req, res, next) => {

  // name of the file "index"
  res.render("index", {
        msg: "Failure!",
        msg2: "Success!"});
});

app.listen(3000);
```

<br>
<br>
10. How to pass data from res.render to ejs template file <br>
   
   <br>
    
   render() Takes 2 args

- The name the file
- object- data u want to pass on that file
  <br>
  <br>

11 Common ejs tags

- <% 'Scriptlet' tag, for control-flow, no output, include partials
- <%= print the value, data-obj into the HTML template
- <%- Outputs the unescaped value into the template, show picture
- <%# Comment tag, no execution, no output

# Notice

- Browser can read only 3 things: HTML, CSS, JS
- In ejs template file we transpiled js code on express then send to browser: Dom written on express
- Where as when we send Js script to browser, the script run on browser: DOM written on browser
- ejs Templating 4 question
  - What is the name of the file in res.render("index")
  - what data-obj u want to pass to index file res.render( "index", { key : value } )
  - What is the type of file 2 arg i.e ejs in app.set("view engine", "ejs");
  - Where is the location of this ejs file on machine app.set("views", path.join(\_\_dirname, "views"));
