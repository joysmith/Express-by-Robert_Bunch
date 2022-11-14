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
   Building template every single time then sending to client

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

8. What are View engine<br>
   Ref. 3_rendering_video_21
   <br>
   <br>
9. [View Engine concept: What is EJS templating, and how to install the ejs module ?](https://ejs.co/)
   <br>
   <br>

10. [What is EJS templating, and how to install the ejs module ?](https://ejs.co/)
    <br>
    <br>

11. [What is EJS templating, and how to install the ejs module ?](https://ejs.co/)
    <br>
    <br>

# Notice

- Browser can read only 3 things: HTML, CSS, JS
