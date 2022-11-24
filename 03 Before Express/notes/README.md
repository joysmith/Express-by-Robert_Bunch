> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

<br>

1. What is Networking from dev perspective

- <img src="image%20notes/2%20developer%20perspective.png" width="500">
     <br>
     <br>

2. How packet are sent over, dev perspective

- <img src="image%20notes/1%20data%20transfer%20in%20packet.png" width="500">
   <br>
   <br>

3. Feature of UDP

- <img src="image%20notes/4%20UDP%20feature.png" width="500">
     <br>
     <br>

4. Feature of TCP

- <img src="image%20notes/5%20TCP%20feature.png" width="500">
   <br>
   <br>

5. TCP vs UDP

- <img src="image%20notes/6%20TCP%20vs%20UDP.png" width="500">
   <br>
   <br>

6. Http can send following stuff, informs of packets to other browser

- <img src="image%20notes/8%20http%20can%20send%20following%20.png" width="500">
     <br>
     <br>

7. How do http msg look like

- <img src="image%20notes/9%20how%20do%20http%20msg%20look%20like.png" width="500">
     <br>
     <br>

```
 all is a method, and it takes 2 args:
 1. route
 2. callback to run if the route is requested
app.all("/", (req, res) => {
  // res.send(`<h1>This is the home page</h1>`)
});
```

   <br>
   <br>
3. What are the different kinds of http verbs request<br>
   [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods "mdn")

```
app object has a few methods:
HTTP verbs! REST verbs!
CRUD app cooresponence!
1. get - READ
- DEFAULT for all browsers is get.
2. post - CREATE
3. delete - DELETE
4. put - UPDATE
5. all - i will accept any http verbs method mention above

These methods Take 2 args:
1. path
2. callback to run if an HTTP request that matchs THIS verb is made to the path in #1
app.all('/', ( req, res ) => {})

Basic routing with diff. http request
app.get( "/", ( req, res ) => {});

app.post( "/", ( req, res ) => {});

app.delete( "/", ( req, res ) => {});

app.put( "/", ( req, res ) => {});
```

   <img src="Image%20notes/1%20kinds%20of%20http%20request%20.png" width="1000">
   <br>
   <br>

4. How to serve static file from express server<br>
   [Serving static files in Express
   ](https://expressjs.com/en/4x/api.html#express.static "expressjs")

```
app comes with a use method to mount middlewares
use takes 1 arg (right now):
1. the middleware you want to run
app.use(express.static('public'))
```

<br>
<br>

5. How to serve file from machine path using res.sendfile() method, using native path module<br>
   [Serving files from machine path
   ](https://expressjs.com/en/4x/api.html#res.sendFile "expressjs")

```
const path = require("path");

app.all("/", ( req, res ) => {
    console.log(path.join( __dirname + "/node.html" ));
    res.sendFile(path.join( __dirname + "/node.html" ));
});
```

In order to tell node where the files are we need the entire path as it is on this MACHINE, not where the file is relative to server
<br>
<br>

1. [What is Networking from dev perspective]()
   <br>
   <br>
