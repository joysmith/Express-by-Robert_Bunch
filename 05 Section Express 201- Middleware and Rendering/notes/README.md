> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

1. What are middleware <br>
   Express is 2 things

   1. Router
   2. Middleware that comprises a webframework

   Req ---MIDDLEWARE---> Res<br>
   Middleware function is ANY function that has access to the req, res, next object.

   - Request comes in.
   - We need to validate the user, sometimes.
   - We need to store some things in the DB.
   - If there is data from the user we need to parse it and store it
   - Res goes out
     <br>
     <br>

2. How to post data from client to server with security using express middleware method

   [app.use(helmet())](https://www.npmjs.com/package/helmet) <br>
   [app.use(express.static('public'))](https://expressjs.com/en/4x/api.html#express.static) <br>
   [app.use(express.json())](https://expressjs.com/en/4x/api.html#express.json) <br>
   [app.use(express.urlencoded({extended:false}));](https://expressjs.com/en/4x/api.html#express.urlencoded)
   <br>
   <br>

3. How to simulate post request using postman<br>

   - Anytime we need to respond with json, we use [res.json()](https://expressjs.com/en/4x/api.html#res.json), not res.send
   - Anytime we need to respond with HTML, we use res.render()
     <br>
     <br>
     Select x-www-form-urlencoded
     <br>
     <img src="image%20notes/7%20url%20encoder.png" width="700">
     <br>
     Write on key: calue pair to send data  
     <br>
     <img src="image%20notes/8%20key%20value%20in%20body.png" width="700">
     <br>
     <br>

4. What make up server-concept<br>
   <img src="image%20notes/1%20server%20concept.png" width="700">
   <br>
   <br>

5. Server side rendering VS APIs<br>
   <img src="image%20notes/5%20choose%20ur%20weapon.png" width="700">
   <img src="image%20notes/2%20chose%20ur%20weapon.png" width="700">
   <br>
   <br>

6. Working of Server side rendering<br>
   Building template every single time then sending to client<br>
   In server side rendering we can use cookies, session

   - [My Space](https://myspace.com/discover/featured)
   - [Wikipedia](https://en.wikipedia.org/wiki/Express.js)
     <br>
     <img src="image%20notes/4%20server%20side%20rendering.png" width="700">
     <img src="image%20notes/6%20my%20space.png" width="700">
     <br>
     <br>

7. Working of JSON APIs<br>
   Sending HTML,CSS,JS on first load, then update the DOM by JSON

   - [Facebook](https://www.facebook.com/)
   - [Amazon](https://www.amazon.com/)
     <br>
     <img src="image%20notes/3%20JSON%20APIs.png" width="700">
     <br>
     <br>

8. How to setup View engine<br>

   1. Express as we know it happens. This File.
   2. We define a view engine.
      - EJS
      - Mustache
      - Handlebars
      - Jade/Pug
   3. Inside one of our routes, we have a res.render
   4. We pass that res.render 2 things:
      - the file we want to use.
      - the data we want to send to that file
   5. Express uses the node module for our specified view engine and parses the file.
      - that means, it takes the HTML/JS/CSS and combines it with whatever "node" there is in the file
   6. The final result of this process is a compiled product of the things the browser can read.
      - HTML, JS, CSS.

   <br>
   <br>

9. View Engine concept: What is EJS templating, and how to [install the ejs](https://ejs.co/) module ?
   <br>
   <br>

10. [app.set()](https://expressjs.com/en/api.html#app.set), takes 2 args<br>

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
   
   [res.render()](https://expressjs.com/en/api.html#res.render) <br>
    
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
