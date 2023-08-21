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

<br>

### 28. Getting data from the query string<a id="28"></a>

<br>

### 29. Getting data from params (URL wildcards) - req.params and req.param()<a id="29"></a>

<br>

### 30. Sending files, and headers already sent!<a id="30"></a>

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

35. How to redirect user from post route by using [res.redirect()](https://expressjs.com/en/api.html#res.redirect) method after data submission
    <br>
    <br>

36. How to save data using cookie by [res.cookie()](https://expressjs.com/en/api.html#res.cookie) method <br>
    <br>
    <br>

37. How to clear cookie data by [ res.clearCookie ?](https://expressjs.com/en/api.html#res.clearCookie)<br>
    <br>
    <br>

38. How to remove cookie data from chrom<br>
    <img src="notes/1%20how%20to%20delete%20cookie%20data.png" width="700">
    <br>
    <br>

---

5.How to pass data through url using query string<br>

- The "?" mark is a special character in URL
- The ? mark says everything after me is the part of query string and
- Everything before me is the part of actual path of the domain
- we can pass multiple query by using "&" character
- The query string is where you put insecure data
  <img src="notes/4%20url.png" width="700">
  <br>
  <br>

   <img src="notes/6%20google%20url.png" width="700">
   <br>
   <br>
   
   <img src="notes/5%20query%20string%20.png" width="700">
   <br>
   <br>

   <img src="notes/7%20google%20query%20string.png" width="700">
   <br>
   <br>

6. How to use [req.query ](https://expressjs.com/en/api.html#req.query) ?
   <br>
   <br>

---

7. How to send data from url using params

- [How to use req.params property](https://expressjs.com/en/4x/api.html#req.params) ?
- How to use [ req.params()](https://expressjs.com/en/4x/api.html#req.param) ?
- The other way of passing data through url, is by params
- In a route, anytime something has a : in front it is a wildcard!
- wildcard, will match anything in that slot

<img src="notes/8%20param.png" width="700">
  <br>
  <br>

<img src="notes/9%20Use%20of%20param%20in%20espn%20website.png" width="700">
   <br>
   <br>

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
